<img width="525" height="793" alt="image" src="https://github.com/user-attachments/assets/0fac7581-e063-4f6f-91ae-8a630394fcbf" />
# UiPath RPA Web Scraper - W3Schools Customers Table to CSV

An automated Robotic Process Automation (RPA) workflow developed with **UiPath Studio Web** on macOS. The bot automates Google Chrome, extracts tabular customer records directly from the DOM using custom JavaScript injection, and saves an RFC 4180 compliant CSV file formatted for Apple Numbers and Microsoft Excel.

## Features

- **DOM-Based Table Extraction**: Injects a custom JavaScript parser directly into the browser context, eliminating schema mismatch bugs and empty DataTable returns.
- **Cross-Platform Compatibility**: Fully configured and tested under macOS with UiPath Assistant Remote Agent.
- **Clean CSV Output**: Produces structured headers (`Company`, `Contact`, `Country`) with proper quote escaping for seamless viewing in Apple Numbers or Excel.

## Workflow Architecture

1. **Use Browser**: Launches Chrome and opens `https://www.w3schools.com/html/html_tables.asp`.
2. **Inject Js Script**: Executes an in-memory DOM query on `#customers` and formats table rows into a CSV string.
3. **Write Text File**: Outputs the generated string directly to `/Users/srikarthikk/Desktop/w3schools_customers.csv`.

## JavaScript DOM Parser Snippet

```javascript
function(element, input) {
    var rows = document.querySelectorAll('#customers tr');
    var csv = [];
    for (var i = 0; i < rows.length; i++) {
        var cols = rows[i].querySelectorAll('td, th');
        var rowData = [];
        for (var j = 0; j < cols.length; j++) {
            rowData.push('"' + cols[j].innerText.trim().replace(/"/g, '""') + '"');
        }
        csv.push(rowData.join(','));
    }
    return csv.join('\n');
}
How to Run
Clone this repositoy:git clone [https://github.com/srikarthik-dev/UiPath-RPA-WebScraper.git]
Import the project into UiPath Studio Web.

Run the workflow using Debug on local machine.

Open the generated file in Apple Numbers:open -a Numbers ~/Desktop/w3schools_customers.csv
