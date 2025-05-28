# MSS Landing Page

A modern, responsive landing page for your LLC specializing in custom test automation, QA solutions, and React/React Native development.

## Features

- **Responsive Design**: Fully responsive layout that works on all devices
- **Modern UI**: Clean, professional design with smooth animations
- **Interactive Elements**: Hover effects, smooth scrolling, and form validation
- **Service Showcase**: Dedicated sections for services, packages, portfolio, and testimonials
- **Contact Form**: Functional contact form with validation
- **Mobile Navigation**: Hamburger menu for mobile devices
- **Performance Optimized**: Fast loading with optimized assets

## Sections Included

1. **Hero Section**: Eye-catching introduction with call-to-action buttons
2. **Services**: Six key services including test automation, React development, etc.
3. **Packages**: Three pricing tiers (Starter, Professional, Enterprise)
4. **Portfolio**: Four sample projects showcasing your work
5. **Testimonials**: Three client testimonials
6. **Contact**: Contact information and functional contact form
7. **Footer**: Links, social media, and company information

## Quick Start

1. **Clone or Download**: Get all the files in your project directory
2. **Open**: Simply open `index.html` in your web browser
3. **Customize**: Edit the content to match your business details

## Customization Guide

### 1. Company Information

**Update the following in `index.html`:**

- Company name: Replace "MSS" with your company name
- Contact information in the contact section
- Email addresses and phone numbers
- Social media links in the footer

### 2. Services

**Modify the services section:**

- Update service titles and descriptions
- Change icons by replacing Font Awesome classes
- Add or remove service cards as needed

### 3. Packages/Pricing

**Customize pricing packages:**

- Update package names, prices, and features
- Modify the "Most Popular" badge
- Add or remove features from each package

### 4. Portfolio

**Replace sample projects:**

- Update project titles and descriptions
- Change technology tags
- Add real project images (replace placeholder icons)

### 5. Testimonials

**Add real client testimonials:**

- Replace sample testimonials with real ones
- Update client names and companies
- Add real client photos (replace placeholder avatars)

### 6. Colors and Branding

**Update the color scheme in `styles.css`:**

```css
/* Primary gradient colors */
background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);

/* Change to your brand colors */
background: linear-gradient(135deg, #your-color-1 0%, #your-color-2 100%);
```

**Key color variables to update:**

- `#667eea` - Primary blue
- `#764ba2` - Secondary purple
- `#333` - Dark text
- `#666` - Light text
- `#f8f9fa` - Light background

### 7. Typography

**Change fonts in `styles.css`:**

- Current font: Inter (Google Fonts)
- Update the Google Fonts link in `index.html`
- Modify font-family in CSS

### 8. Images

**Add real images:**

- Replace hero graphic with your logo or custom graphic
- Add portfolio project screenshots
- Include team photos for testimonials
- Update favicon

## File Structure

```
├── index.html          # Main HTML file
├── styles.css          # All CSS styles
├── script.js           # JavaScript functionality
└── README.md           # This file
```

## Browser Support

- Chrome (latest)
- Firefox (latest)
- Safari (latest)
- Edge (latest)
- Mobile browsers

## Performance Tips

1. **Optimize Images**: Compress images before adding them
2. **Minify CSS/JS**: Use minification tools for production
3. **CDN**: Consider using a CDN for Font Awesome and Google Fonts
4. **Lazy Loading**: Implement lazy loading for images if adding many

## Deployment

### Option 1: Static Hosting

- Upload files to any static hosting service (Netlify, Vercel, GitHub Pages)
- No server-side requirements

### Option 2: Traditional Web Hosting

- Upload files to your web hosting provider
- Ensure the hosting supports HTML/CSS/JS

### Option 3: Local Development

- Use a local server for development:

  ```bash
  # Python 3
  python -m http.server 8000

  # Node.js (with http-server)
  npx http-server
  ```

## Contact Form Integration

The contact form currently shows a success message without actually sending emails. To make it functional:

### Option 1: Formspree

1. Sign up at [Formspree.io](https://formspree.io)
2. Update the form action in `index.html`:
   ```html
   <form
     class="contact-form"
     action="https://formspree.io/f/YOUR_FORM_ID"
     method="POST"
   ></form>
   ```

### Option 2: Netlify Forms

1. Add `netlify` attribute to the form:
   ```html
   <form class="contact-form" netlify></form>
   ```

### Option 3: Custom Backend

- Implement your own form handler
- Update the JavaScript in `script.js` to send to your endpoint

## SEO Optimization

1. **Meta Tags**: Add relevant meta descriptions and keywords
2. **Alt Text**: Add alt attributes to images
3. **Schema Markup**: Consider adding structured data
4. **Sitemap**: Create a sitemap.xml file
5. **Analytics**: Add Google Analytics or similar

## Accessibility

The landing page includes basic accessibility features:

- Semantic HTML structure
- Keyboard navigation support
- Focus indicators
- Alt text for icons (when images are added)

## Support

For questions or customization help:

- Review the code comments
- Check browser developer tools for any errors
- Ensure all files are in the same directory

## License

This landing page template is provided as-is for your business use. Feel free to modify and customize as needed.

---

**Note**: Remember to update all placeholder content with your actual business information before going live!
