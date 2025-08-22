# Static Website (GitHub Pages)

**ALWAYS follow these instructions first and fallback to additional search and context gathering only when the information here is incomplete or found to be in error.**

This repository hosts a simple static website (HTML + CSS, optional light JS) served directly via GitHub Pages. There is no backend, no database, and no build pipeline required. All content changes are requested through GitHub Issues and implemented via pull requests.

## Working Effectively

### Environment Setup
- No build process required - this is a purely static website
- Required tools available in environment:
  - Python 3.12.3+ for local development server
  - Node.js 20.19.4+ for optional validation tools
- Repository structure:
  ```
  index.html
  assets/
    css/
      styles.css
  README.md
  .github/
    copilot-instructions.md
  ```

### Local Development and Testing
- **ALWAYS** start with local preview for any changes:
  ```bash
  cd /home/runner/work/website/website
  python3 -m http.server 8000
  ```
  - Server starts in ~2 seconds
  - Visit: http://localhost:8000
  - NEVER CANCEL - server runs continuously until stopped

### Validation Commands
Run these validation steps for ALL changes:

1. **Local Server Test** (MANDATORY):
   ```bash
   cd /home/runner/work/website/website
   python3 -m http.server 8000 &
   SERVER_PID=$!
   sleep 3
   curl -s http://localhost:8000/ | head -5
   curl -s http://localhost:8000/assets/css/styles.css | head -3
   kill $SERVER_PID
   ```
   - Expected: HTML and CSS content returned successfully
   - Time: ~10 seconds total

2. **HTML Validation** (RECOMMENDED):
   ```bash
   cd /home/runner/work/website/website
   npx html-validate index.html
   ```
   - Time: ~15 seconds (includes package download)
   - NEVER CANCEL - wait for npm package installation
   - Note: May show style warnings about self-closing tags (non-functional issues)
   - Expected: HTML structure validates, ignore void-style warnings

3. **Manual Browser Testing** (MANDATORY):
   - Start local server: `python3 -m http.server 8000`
   - Navigate to: http://localhost:8000
   - Verify: Page loads with "Hello World" heading and tagline
   - Verify: CSS styling applies (dark theme by default, light theme based on system preference)
   - Take screenshot to document visual changes

### Content Change Workflow
**CRITICAL**: Never push directly to `main`. Every change follows this pattern:

1. **Issue-Driven Process**:
   - All changes originate from GitHub Issues
   - Issues describe exact content changes needed
   - Agent creates branch + pull request implementing the change

2. **Change Implementation**:
   - Edit `index.html` for content changes
   - Edit `assets/css/styles.css` for styling changes
   - Keep HTML semantic and accessible
   - Maintain clean, minimal structure

3. **Testing Requirements**:
   - ALWAYS run local server validation
   - ALWAYS test in browser manually
   - ALWAYS take screenshot of visual changes
   - Run HTML validation (ignore style warnings)

## Validation Scenarios

### Complete User Testing Flow
After making any changes, ALWAYS execute this complete scenario:

1. **Static Server Validation**:
   ```bash
   cd /home/runner/work/website/website
   python3 -m http.server 8000 &
   SERVER_PID=$!
   sleep 2
   ```

2. **Content Loading Test**:
   ```bash
   curl -f http://localhost:8000/ > /dev/null && echo "✓ HTML loads"
   curl -f http://localhost:8000/assets/css/styles.css > /dev/null && echo "✓ CSS loads"
   ```

3. **Visual Verification**:
   - Navigate browser to http://localhost:8000
   - Verify page renders correctly
   - Check both light and dark theme rendering
   - Take screenshot for documentation

4. **Cleanup**:
   ```bash
   kill $SERVER_PID
   ```

### Content Verification Checklist
For every change, verify:
- [ ] HTML is valid semantic markup
- [ ] CSS loads and applies correctly
- [ ] Site displays "Hello World" heading (or updated content)
- [ ] Footer shows "© 2025" (or current year)
- [ ] Responsive design works on different viewport sizes
- [ ] Both light and dark color schemes function
- [ ] All relative paths resolve correctly

## Technology Constraints

### What Works
- Pure HTML5 + CSS3
- Semantic markup with accessibility features
- CSS prefers-color-scheme for light/dark themes
- Python HTTP server for local development
- npx html-validate for HTML validation
- Static asset serving via GitHub Pages

### What Does NOT Work / Avoid
- No build process - do not try to add bundlers, npm scripts, or build tools
- No server-side rendering - site is purely static
- No databases or external services
- No client-side frameworks - keep pure HTML/CSS/minimal JS
- CSS validation requires configuration - focus on manual testing instead

## Critical Timing and Timeouts

### Command Timing Expectations
- Local server startup: 2 seconds
- HTML validation: 15 seconds (NEVER CANCEL - includes npm download)
- Manual browser testing: 5-10 seconds
- Asset loading verification: 5 seconds

### NEVER CANCEL Commands
- `python3 -m http.server 8000` - runs until manually stopped
- `npx html-validate` - may take 15+ seconds for package download
- Any npm package installation via npx - wait for completion

## Common Tasks Reference

### Repository Root Contents
```
/home/runner/work/website/website/
├── index.html                    # Main website page
├── assets/
│   └── css/
│       └── styles.css           # All styling
├── README.md                    # Project documentation
└── .github/
    └── copilot-instructions.md  # This file
```

### Working Commands Quick Reference
```bash
# Start local development
cd /home/runner/work/website/website
python3 -m http.server 8000

# Validate HTML
npx html-validate index.html

# Test asset loading
curl http://localhost:8000/assets/css/styles.css

# Quick content verification
curl -s http://localhost:8000/ | grep -E "<title>|<h1>"
```

### Key Files to Monitor
- `index.html` - Main content and structure
- `assets/css/styles.css` - All visual styling
- Always maintain semantic HTML structure
- Always preserve accessibility features (proper headings, alt text)

## Error Handling

### Common Issues and Solutions
- **"Address already in use" on port 8000**: Kill existing server with `pkill -f "python3 -m http.server"`
- **CSS not loading**: Verify file exists at `assets/css/styles.css` and check relative paths
- **HTML validation warnings**: Self-closing tag style warnings are non-functional, site works correctly
- **Slow npx commands**: Wait for completion - npm package downloads are normal

### Debugging Steps
1. Verify file structure matches expected layout
2. Test local server starts successfully
3. Check browser developer tools for asset loading errors
4. Validate HTML structure using npx html-validate
5. Confirm CSS applies by inspecting computed styles

**Remember**: This is an intentionally simple static website. Resist adding complexity unless explicitly requested via GitHub Issue.