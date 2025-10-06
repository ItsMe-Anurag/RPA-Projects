

# RPA Projects – Web Scraping, Data Extraction & Automation

This repository contains RPA (UiPath) projects that perform web scraping from the **UiPath ACME** demo site, process and filter the data, extract additional details using regex, and send an email with the final results.

---

## 🧠 Project Description & Use Case

In this automation:

1. The robot navigates through the **ACME UiPath demo** website, going through multiple pages of **work items**.
2. It scrapes data (e.g. work item ID, title, status, etc.) for each page and aggregates into Excel.
3. Applies filters to the scraped data according to given conditions.
4. For each filtered work item, opens a URL constructed with its **WIID (Work Item ID)**, extracts the **Client ID** using **regular expressions**.
5. Finally, attaches the resulting filtered Excel file and emails it to a recipient.

This process automates a complete cycle: extraction → transformation → enrichment → delivery.

---

## 📁 Folder Structure

```
/ (root)
├── ProjectFile.xaml # Main workflow of scraping → filtering → extraction → mail
├── Config/ # Configuration files
│ └── Config.xlsx # Settings: base URL, filters, email settings, regex patterns, etc.
├── Data/
│ ├── ScrapedData.xlsx # Raw scraped data
│ ├── FilteredData.xlsx # Filtered & enriched output
│ └── Temp/ # Temporary files if needed
├── Helpers/ # Utility workflows
│ ├── NavigatePages.xaml
│ ├── ScrapePage.xaml
│ ├── FilterData.xaml
│ ├── ExtractClientID.xaml
│ └── SendMail.xaml
├── Documentation/ # Any supporting docs/screenshots
├── Tests/ # Test workflows / small modules
└── project.json
```

You can adapt or expand based on your actual structure.

---

## ⚙️ Prerequisites

- **UiPath Studio** (compatible version)
- Necessary activity packages:
  - UiPath.Web.Activities
  - UiPath.Excel.Activities
  - UiPath.Mail.Activities
- Network access to the ACME site
- Email SMTP server or configured email settings
- Permissions to write files / send email
- Regex knowledge or correct patterns in config for extracting client IDs

---

## 🚀 Setup & Configuration

1. Clone or download the repository.
2. Open the project in UiPath Studio.
3. In `Config/Config.xlsx`, configure:
   - Base URL of ACME site
   - Pagination parameters (page count, selectors)
   - Filter criteria (e.g. status, date, etc.)
   - Regex pattern(s) for Client ID extraction
   - Email settings (SMTP server, sender, recipient, subject, body)
4. Ensure Excel file paths (ScrapedData, FilteredData) exist or create them.
5. Test helper workflows (in `Tests/`) to validate scraping, filtering, extraction modules.

---

## 🧩 Workflow Overview

Here’s a high-level flow of the automation:

1. **Initialization**  
   - Read config values (URLs, filters, regex, email settings).  
   - Initialize logging, file paths.

2. **Navigate & Scrape**  
   - Loop through pages of the ACME work items list.  
   - For each page:
     - Extract work item rows and fields (e.g. ID, name, status).  
     - Append to `ScrapedData.xlsx`.

3. **Filter Data**  
   - Read the scraped file.  
   - Apply filter conditions (e.g. status = “Pending”, date threshold).  
   - Save filtered entries to `FilteredData.xlsx`.

4. **Extract Client ID for Each Work Item**  
   - For each work item in filtered list:
     - Construct URL using its WIID (e.g. `baseURL + "/workitem/" + WIID`).  
     - Navigate to that URL.  
     - Extract text (HTML, JSON, etc.).  
     - Use regex to find **Client ID**.  
     - Add Client ID into the filtered data table.

5. **Send Email**  
   - Attach `FilteredData.xlsx`.  
   - Using configured email settings, send the final report.

6. **Cleanup & Logging**  
   - Close browser, Excel applications.  
   - Log success/failures, exception screenshots if any.

---

## 🧪 Testing

- Use workflows in `Tests/` to individually validate:
  - Pagination & scraping logic  
  - Filtering logic  
  - Regex extraction of Client ID  
  - Email sending  
- Create sample dummy data and run modules in isolation to catch logic bugs before full end-to-end run.

---

## 📜 License

This project is licensed under the **MIT License** — see the included [LICENSE](LICENSE) file for details.

---

## 🙏 Credits / Acknowledgements

- Built using **UiPath Studio** and standard Web / Excel / Mail activities.
- Inspired by real-world RPA tasks around data extraction and report generation.
- Created & maintained by **[ItsMe-Anurag](https://uithub.com/ItsMe-Anurag)**.

---




