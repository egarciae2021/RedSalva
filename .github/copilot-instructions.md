# RedSalva - Clínica Montesur Website

RedSalva (www.redsalva.com) is a static HTML website for Clínica Montesur, a medical clinic in Peru. The site contains information about medical specialties, staff, and services. This is a WordPress-exported static site hosted on GitHub Pages.

Always reference these instructions first and fallback to search or bash commands only when you encounter unexpected information that does not match the info here.

## Working Effectively

### Repository Structure
```
.
├── index.html              # Main landing page with SVG background
├── principal.html          # Main content page (WordPress-exported)  
├── especialidades.html     # Medical specialties page
├── staff.html              # Staff/doctors page
├── CNAME                   # Domain configuration (www.redsalva.com)
├── README.md               # Basic project info
├── fondo.svg               # Large background SVG (3MB)
├── logo.jpg, logo2.png     # Logo assets
├── dbInvoicing.bak         # SQL Server database backup (do not modify)
├── web2_files/             # CSS/JS assets for main site
├── especialidades_files/   # Assets for specialties page
└── staff_files/            # Assets for staff page
```

### Local Development and Testing
- Start local development server: `python3 -m http.server 8080`
- Server starts in < 1 second. NEVER CANCEL - let it complete startup.
- Access site at: `http://localhost:8080/`
- Test all main pages:
  - `http://localhost:8080/index.html` - Landing page (736 bytes, loads in ~0.003s)
  - `http://localhost:8080/principal.html` - Main content (516KB, loads in ~0.002s)
  - `http://localhost:8080/especialidades.html` - Specialties (518KB, loads in ~0.002s)  
  - `http://localhost:8080/staff.html` - Staff page (350KB, loads in ~0.001s)
- Stop server: `Ctrl+C` or `pkill -f "python3 -m http.server"`

### Build Process
- **NO BUILD PROCESS REQUIRED** - This is a static HTML website
- Files are served directly as-is from the repository
- No package.json, Makefile, or build scripts exist
- No dependencies to install or compile

### Deployment
- Deployment is automatic via GitHub Pages
- Push changes to any branch and GitHub Pages will update the live site
- Live site: https://www.redsalva.com (configured via CNAME file)
- Deployment typically takes 1-2 minutes after push

## Validation

### Essential Validation Steps
ALWAYS run these validation steps after making any changes:

1. **Local Testing (takes ~3 seconds total)**:
   ```bash
   # Start server, test all pages, stop server
   python3 -m http.server 8080 > /tmp/server.log 2>&1 & SERVER_PID=$!
   sleep 2
   curl -s http://localhost:8080/index.html > /dev/null && echo "✓ index.html loads"
   curl -s http://localhost:8080/principal.html > /dev/null && echo "✓ principal.html loads"
   curl -s http://localhost:8080/especialidades.html > /dev/null && echo "✓ especialidades.html loads"
   curl -s http://localhost:8080/staff.html > /dev/null && echo "✓ staff.html loads"
   kill $SERVER_PID
   ```

2. **HTML Validation (takes ~3-4 seconds per file)**:
   ```bash
   # Install validator (first time only, takes ~30 seconds)
   pip3 install html5validator
   
   # Validate modified HTML files
   html5validator index.html
   html5validator principal.html  # May show CSS warnings (expected)
   html5validator especialidades.html
   html5validator staff.html
   ```

3. **Manual Testing Scenarios**:
   - ALWAYS verify the SVG background loads correctly on index.html
   - Check that images (logos) display properly on all pages
   - Verify navigation links work between pages
   - Test on both desktop and mobile viewport sizes
   - Confirm Spanish text displays correctly (UTF-8 encoding)

### Expected Validation Results
- Local server starts successfully in < 1 second
- All pages return HTTP 200 status
- Total validation time: ~10-15 seconds for complete test suite
- HTML validator may show CSS warnings on WordPress-exported pages - this is expected and acceptable

## Development Guidelines

### File Editing
- Edit HTML files directly - no preprocessing needed
- CSS/JS assets in `*_files/` directories are from WordPress export - avoid modifying unless necessary  
- Main editable files: `index.html`, `principal.html`, `especialidades.html`, `staff.html`
- Always preserve UTF-8 encoding for Spanish text content
- Maintain existing meta tags and SEO structure

### Common Tasks
- **Adding new content**: Edit HTML files directly using standard HTML5 syntax
- **Styling changes**: Modify inline styles or reference existing CSS in `*_files/` directories
- **Image updates**: Replace image files and update HTML references
- **SEO updates**: Modify meta tags in `<head>` sections

### Do Not Modify
- Database backup file (`dbInvoicing.bak`) 
- CNAME file (controls domain configuration)
- Asset directories (`*_files/`) unless specifically needed for your change
- WordPress-generated CSS/JS files without careful testing

### Testing New Changes
1. Edit HTML files
2. Run local validation (3-second test script above)
3. Test in browser at `localhost:8080`
4. Verify content displays correctly in Spanish
5. Push changes to trigger GitHub Pages deployment
6. Verify live site updates at www.redsalva.com within 2-3 minutes

## Troubleshooting

### Common Issues
- **Port 8080 in use**: Change port number: `python3 -m http.server 8081`
- **Pages not loading**: Check file permissions and ensure server started successfully
- **SVG not displaying**: Verify `fondo.svg` file exists and path is correct in `index.html`
- **Spanish characters broken**: Ensure UTF-8 encoding in HTML files

### Performance Notes
- Large pages (especialidades.html, principal.html) are 500KB+ due to WordPress export
- fondo.svg is 3MB - this is expected for the background graphic
- Site loads quickly despite file sizes due to static hosting

This website is optimized for GitHub Pages hosting and requires no complex build processes or dependencies.