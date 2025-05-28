# Analytics & Tracking Setup Guide

This guide covers multiple analytics solutions you can implement on your MSS landing page, especially optimized for Azure deployment.

## 🎯 Recommended Analytics Stack

### **Primary: Google Analytics 4 + Microsoft Clarity**

- **GA4**: Demographics, traffic sources, conversions
- **Clarity**: Heatmaps, session recordings, user behavior

## 📊 Analytics Options

### **1. Google Analytics 4 (GA4)**

**What you get:**

- Demographics (age, gender, interests)
- Geographic data (country, city, region)
- Device information (mobile, desktop, browser)
- Traffic sources (organic, direct, referral, social)
- Real-time visitor data
- Conversion tracking
- Custom events

**Setup:**

1. Go to [Google Analytics](https://analytics.google.com)
2. Create account → Create property
3. Get your Measurement ID (format: G-XXXXXXXXXX)
4. Replace `GA_MEASUREMENT_ID` in `index.html` with your actual ID

**Cost:** Free (up to 10M events/month)

### **2. Microsoft Clarity** ⭐ _Perfect for Azure_

**What you get:**

- Session recordings (watch actual user sessions)
- Heatmaps (click, scroll, area attention)
- User behavior insights
- Performance metrics
- Mobile app analytics
- Integrates with Azure Application Insights

**Setup:**

1. Go to [Microsoft Clarity](https://clarity.microsoft.com)
2. Create project
3. Get your Project ID
4. Replace `CLARITY_PROJECT_ID` in `index.html`

**Cost:** Free (unlimited)

### **3. Azure Application Insights** 🔥 _Azure Native_

**What you get:**

- Real-time performance monitoring
- Custom telemetry
- User flows and funnels
- Geographic distribution
- Browser and OS analytics
- Integration with Azure services

**Setup Options:**

#### **Option 1: CDN Import (Recommended for Static Sites)**

```html
<!-- Add to head section -->
<script src="https://js.monitor.azure.com/scripts/b/ai.2.min.js"></script>
<script>
  var appInsights =
    window.appInsights ||
    (function (a) {
      function b(a) {
        c[a] = function () {
          var b = arguments;
          c.queue.push(function () {
            c[a].apply(c, b);
          });
        };
      }
      var c = { config: a },
        d = document,
        e = window;
      setTimeout(function () {
        var b = d.createElement("script");
        b.src = a.url || "https://az416426.vo.msecnd.net/scripts/b/ai.2.min.js";
        d.getElementsByTagName("head")[0].appendChild(b);
      });
      try {
        c.cookie = d.cookie;
      } catch (a) {}
      (c.queue = []), (c.version = 2);
      for (
        var f = [
          "Event",
          "PageView",
          "Exception",
          "Trace",
          "DependencyData",
          "Metric",
          "PageViewPerformance",
        ];
        f.length;

      )
        b("track" + f.pop());
      b("startTrackPage"), b("stopTrackPage");
      var g = "Track" + f[0];
      if (
        (b("start" + g),
        b("stop" + g),
        b("addTelemetryInitializer"),
        b("setAuthenticatedUserContext"),
        b("clearAuthenticatedUserContext"),
        b("flush"),
        !(
          !0 === a.disableExceptionTracking ||
          (a.extensionConfig &&
            a.extensionConfig.ApplicationInsightsAnalytics &&
            !0 ===
              a.extensionConfig.ApplicationInsightsAnalytics
                .disableExceptionTracking)
        ))
      ) {
        b("_" + (f = "onerror"));
        var h = e[f];
        (e[f] = function (a, b, d, e, g) {
          var i = h && h(a, b, d, e, g);
          return (
            !0 !== i &&
              c["_" + f]({
                message: a,
                url: b,
                lineNumber: d,
                columnNumber: e,
                error: g,
              }),
            i
          );
        }),
          (a.autoExceptionInstrumented = !0);
      }
      return c;
    })({
      instrumentationKey: "YOUR_INSTRUMENTATION_KEY",
    });

  // Initialize
  appInsights.loadAppInsights();
  appInsights.trackPageView();
</script>
```

#### **Option 2: Modern ES6 Module (For Build Systems)**

```javascript
// Install: npm install @microsoft/applicationinsights-web

import { ApplicationInsights } from "@microsoft/applicationinsights-web";

const appInsights = new ApplicationInsights({
  config: {
    instrumentationKey: "YOUR_INSTRUMENTATION_KEY",
    enableAutoRouteTracking: true, // Auto track route changes
    enableCorsCorrelation: true,
    enableRequestHeaderTracking: true,
    enableResponseHeaderTracking: true,
  },
});

appInsights.loadAppInsights();
appInsights.trackPageView();

// Export for use in other files
export default appInsights;
```

#### **Option 3: Simple CDN + Config (Cleanest for Static Sites)**

```html
<!-- In head section -->
<script src="https://js.monitor.azure.com/scripts/b/ai.2.min.js"></script>
<script>
  // Simple configuration
  window.appInsights = new Microsoft.ApplicationInsights.ApplicationInsights({
    config: {
      instrumentationKey: "YOUR_INSTRUMENTATION_KEY",
      enableAutoRouteTracking: true,
      disableFetchTracking: false,
      enableCorsCorrelation: true,
    },
  });

  appInsights.loadAppInsights();
  appInsights.trackPageView();
</script>
```

### **4. Hotjar** 💰 _Premium Alternative_

**What you get:**

- Advanced heatmaps
- Session recordings
- Conversion funnels
- Form analytics
- Feedback polls
- User surveys

**Cost:** $32/month (basic plan)

### **5. Mixpanel** 💰 _Event-Focused_

**What you get:**

- Advanced event tracking
- User journey analysis
- Cohort analysis
- A/B testing
- Real-time analytics

**Cost:** Free (up to 1000 users), then $25/month

## 🌍 Geographic & Demographic Data

### **What Each Tool Provides:**

| Tool             | Location Data         | Demographics           | Device Info         | Behavior             |
| ---------------- | --------------------- | ---------------------- | ------------------- | -------------------- |
| **GA4**          | Country, Region, City | Age, Gender, Interests | Browser, OS, Device | Page views, Events   |
| **Clarity**      | Country, Region       | -                      | Browser, OS, Device | Heatmaps, Recordings |
| **App Insights** | Country, Region       | -                      | Browser, OS, Device | Performance, Errors  |
| **Hotjar**       | Country               | -                      | Browser, OS, Device | Advanced Heatmaps    |

## 🔧 Azure-Specific Setup

### **For Azure Static Web Apps:**

1. **Application Insights Integration:**

```javascript
// Add to your script.js
function initAzureInsights() {
  if (typeof appInsights !== "undefined") {
    // Track page view (already done automatically)

    // Track custom events
    appInsights.trackEvent({
      name: "page_loaded",
      properties: {
        page: window.location.pathname,
        timestamp: new Date().toISOString(),
        userAgent: navigator.userAgent,
      },
    });

    // Track form submissions
    appInsights.trackEvent({
      name: "contact_form_view",
      properties: {
        section: "contact",
      },
    });
  }
}

// Enhanced tracking functions
function trackAppInsightsEvent(eventName, properties = {}) {
  if (typeof appInsights !== "undefined") {
    appInsights.trackEvent({
      name: eventName,
      properties: {
        ...properties,
        timestamp: new Date().toISOString(),
        page: window.location.pathname,
      },
    });
  }
}

// Call on page load
document.addEventListener("DOMContentLoaded", initAzureInsights);
```

2. **Environment Variables in Azure:**

```json
// In your Azure Static Web App configuration
{
  "environmentVariables": {
    "GA_MEASUREMENT_ID": "G-XXXXXXXXXX",
    "CLARITY_PROJECT_ID": "your-clarity-id",
    "APPINSIGHTS_INSTRUMENTATIONKEY": "your-key"
  }
}
```

## 📈 Custom Events Already Implemented

Your landing page now tracks:

- **Page Views**: Automatic tracking
- **Section Views**: When users scroll to different sections
- **Button Clicks**: All CTA buttons with location context
- **Form Interactions**: Field focus, submission attempts, errors
- **Navigation**: Menu clicks, internal links
- **Mobile Usage**: Hamburger menu interactions

## 🎯 Conversion Goals to Set Up

1. **Contact Form Submission** (Primary Goal)
2. **Package Button Clicks** (Micro-conversions)
3. **Portfolio Item Views** (Engagement)
4. **Service Section Views** (Interest indicators)
5. **Phone/Email Clicks** (Direct contact intent)

## 🚀 Quick Start Checklist

### **Immediate Setup (5 minutes):**

- [ ] Create Google Analytics 4 account
- [ ] Replace `GA_MEASUREMENT_ID` in index.html
- [ ] Create Microsoft Clarity account
- [ ] Replace `CLARITY_PROJECT_ID` in index.html

### **Azure Integration (10 minutes):**

- [ ] Set up Application Insights in Azure
- [ ] Add instrumentation key to your Static Web App
- [ ] Configure environment variables

### **Advanced Setup (30 minutes):**

- [ ] Set up conversion goals in GA4
- [ ] Configure custom dimensions
- [ ] Set up automated reports
- [ ] Create dashboards

## 📊 What You'll See

### **Demographics:**

- Age ranges of visitors
- Geographic distribution
- Device preferences (mobile vs desktop)
- Browser usage

### **Behavior:**

- Most viewed sections
- Button click rates
- Form completion rates
- Time spent on page
- Scroll depth

### **Traffic Sources:**

- Direct traffic
- Search engines
- Social media
- Referral sites

## 🔒 Privacy Considerations

### **GDPR/CCPA Compliance:**

```html
<!-- Add cookie consent banner -->
<div id="cookie-banner" style="display: none;">
  <p>
    We use cookies to improve your experience.
    <a href="#privacy">Privacy Policy</a>
  </p>
  <button onclick="acceptCookies()">Accept</button>
</div>

<script>
  function acceptCookies() {
    localStorage.setItem("cookies-accepted", "true");
    document.getElementById("cookie-banner").style.display = "none";
    // Initialize analytics only after consent
    initAnalytics();
  }

  // Check consent on load
  if (!localStorage.getItem("cookies-accepted")) {
    document.getElementById("cookie-banner").style.display = "block";
  } else {
    initAnalytics();
  }
</script>
```

## 💡 Pro Tips

1. **Start Simple**: Begin with GA4 + Clarity (both free)
2. **Azure Native**: Use Application Insights for Azure-specific features
3. **Mobile Focus**: 60%+ of traffic will likely be mobile
4. **Form Optimization**: Track where users drop off in your contact form
5. **A/B Testing**: Test different headlines, button colors, pricing

## 🎯 Expected Insights

After 1-2 weeks, you'll see:

- **Geographic hotspots** for your services
- **Peak traffic times** for optimal posting
- **Device preferences** for design optimization
- **Popular services** based on section engagement
- **Conversion bottlenecks** in your funnel

Would you like me to help you set up any specific analytics tool or create custom tracking for particular user actions?
