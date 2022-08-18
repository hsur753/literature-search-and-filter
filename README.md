# Literature Search and Filter
A Python tool to streamline literature screening using automated filtering by page limit, language, duplicates and boolean-logic-based keyword search.

Supported Databases: 
- ACM Digital Library
- IEEE Xplore
- ScienceDirect

### Getting Started
Export your database search results as BibTex files and place them in a suitable directory.

Supported Python version >= `3.10.0`.
Install the dependencies by running the following command.
```
pip install requirements.txt
```

### Usage

Run `python main.py` with the below arguments.

| Argument | Value | Required |
|---|---|---|
| --file_path | Path to your BibTex Directory | &check; |
| --mode | "acm", "ieee", "scdrt" | &check; |
| --page_limit | Preferred Minimum Page Count | &check; |
| --excel_path | Path to Output Excel File | &cross; |
| --search_keywords | None | &cross; |

On completion, an Excel file will be created containing the information (Author, Title, DOI URL) on literature that successfully passed the screening process.
If `--excel_path` is specified, the selected Excel workbook will be appended with the results of the screening process; this may be useful if using multiple databases in a single literature review. Otherwise, a new file will be created.

#### Keyword Boolean Logic

If using the keyword search functionality, the tool will prompt you to do the following:
- Enter required keywords separated by a comma (,) to run OR operator.
- Add keywords on a newline to run AND operator or type "X" to finish.
- To search for an exact match of a keyword, enclose it within quotes (" ")

For example, the Boolean logic `("Technology" OR "Computer" OR "Computers" OR "Computing") AND ("Program" OR "Programs" OR "Programming" OR "Coding")` would be entered as:
```
"Technology", Comput
Program, "Coding"
X
```

### Advanced Usage

The tool, by default, filters for publications in English whose Title and Abstract satisfy the defined conditions.
Slight modifications to the source code can allow for a more fine-grained search strategy.

Language Criteria:
```
condition = lambda entry: page_key in entry and (int) (entry[page_key]) >= PAGE_LIMIT and detect(entry[title_key]) == "en"
```

Publication Data Extraction:
```
extract_text = lambda entry: " ".join([entry.get("abstract", ""), entry.get("title", ""), entry.get("keywords", "")])
```
