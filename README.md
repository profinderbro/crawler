# Web Archiver ([Try Now](https://colab.research.google.com/github/profinderbro/crawler/blob/main/crawler.ipynb))

A powerful web crawler and archiver built with Python that can handle dynamic content, lazy loading, and loading screens. This tool creates offline archives of web pages with all their assets (CSS, JavaScript, images, fonts).

## Features

- **Dynamic Content Support**: Handles JavaScript-rendered content using Selenium WebDriver
- **Loading Screen Detection**: Automatically waits for loading screens and spinners to disappear
- **Asset Archiving**: Downloads and saves CSS, JavaScript, images, fonts, and other assets
- **Lazy Loading Handling**: Scrolls through pages to trigger lazy-loaded content
- **Network Idle Detection**: Waits for all network requests to complete
- **Offline Browsing**: Creates fully functional offline archives

## Requirements

- Python 3.7+
- Chrome/Chromium browser
- Internet connection for initial setup

## Installation

### For Google Colab
The notebook includes all necessary installation commands. Simply run the first cell to install dependencies.

### For Local Development
```bash
pip install selenium beautifulsoup4 requests pillow
```

You'll also need to install Chrome/Chromium:
- **Ubuntu/Debian**: `sudo apt-get install chromium-browser`
- **Windows**: Download from [Chrome website](https://www.google.com/chrome/)
- **macOS**: `brew install --cask google-chrome`

## Usage

### Basic Usage
```python
# Initialize the archiver
archiver = EnhancedWebpageArchiver(
    base_url="https://example.com",
    wait_time=10,      # Time to wait for page elements
    scroll_pause=2     # Pause between scrolls
)

# Archive the webpage
archiver.archive_page()
```

### Configuration Options

- `base_url`: The URL of the webpage to archive
- `wait_time`: Maximum time to wait for page elements (default: 10 seconds)
- `scroll_pause`: Time to pause between scroll actions (default: 2 seconds)

## How It Works

1. **Page Loading**: Uses Selenium WebDriver to load the webpage
2. **Dynamic Content**: Waits for JavaScript to execute and content to load
3. **Loading Detection**: Automatically detects and waits for loading screens
4. **Content Scrolling**: Scrolls through the page to trigger lazy-loaded content
5. **Asset Collection**: Identifies and downloads all page assets
6. **Archive Creation**: Saves everything in a structured offline archive

## Output Structure

```
archive_[domain]_[timestamp]/
├── index.html              # Main archived page
├── assets/
│   ├── css/               # Stylesheets
│   ├── js/                # JavaScript files
│   ├── images/            # Images
│   ├── fonts/             # Font files
│   └── other/             # Other assets
```

## Supported Content Types

- **Images**: JPG, PNG, GIF, SVG, WebP
- **Stylesheets**: CSS files and inline styles
- **Scripts**: JavaScript files
- **Fonts**: WOFF, WOFF2, TTF, OTF
- **Other**: Various media and document types

## Loading Screen Detection

The archiver automatically detects common loading indicators:
- Elements with classes containing "loading", "loader", "spinner"
- Elements with IDs containing "loading", "loader"
- Common loading screen classes like "loading-screen", "preloader"

## Network Idle Detection

- Waits for jQuery requests to complete (if jQuery is present)
- Monitors for active network requests
- Ensures all dynamic content has loaded

## Troubleshooting

### Common Issues

1. **Page not loading completely**
   - Increase `wait_time` parameter
   - Check if the site blocks automated browsers

2. **Missing dynamic content**
   - Ensure JavaScript is enabled
   - Increase scroll pause time

3. **Chrome driver issues**
   - Make sure Chrome/Chromium is installed
   - Update Chrome to the latest version

### Error Messages

- `TimeoutException`: Page took too long to load - try increasing wait_time
- `WebDriverException`: Chrome driver issues - check Chrome installation

## Limitations

- Only archives single pages (not entire websites)
- Some heavily protected sites may block automated access
- Large pages with many assets may take significant time to archive
- Some dynamic content may require manual interaction

## Contributing

Feel free to submit issues and enhancement requests!

## License

This project is open source and available under the MIT License.