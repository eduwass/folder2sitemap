# folder2sitemap

## Background
I worked this as a tool that would generate a sitemap from a [webtozip.com](https://webtozip.com) download. 

The download is a zip file that contains the entire website. The website is structured in a way that the root directory contains the index.html file and the rest of the website is structured in directories. 

Each directory contains an index.html file that represents the page. The script scans the directories recursively to build a nested structure of the website. 

The script extracts the title of each page from the `<title>` tag in the HTML files and uses the directory structure to create a hierarchical JSON object representing the site's structure.

## Overview
folder2sitemap is a Node.js script designed to generate a JSON representation of a website's structure based on its directory and file organization. 

It scans a specified directory for HTML files, particularly looking for [index.html](example.com/index.html#1%2C1-1%2C1) files in each directory to determine the structure of the website. 

Note that index.html files ARE REQUIRED for the script to work properly.

The script extracts the title of each page from the `<title>` tag in the HTML files and uses the directory structure to create a hierarchical JSON object representing the site's structure.

## Features
- **Title Extraction**: Extracts titles directly from the HTML files to accurately represent each page.
- **Recursive Directory Traversal**: Scans directories recursively to build a nested structure of the website.
- **JSON Output**: Outputs the website structure in a readable JSON format.
- **CSV Output**: Outputs the website structure in CSV format.
- **Exclusion of Directories**: Allows you to exclude specific directories from the sitemap generation.
- **Custom Output File**: Option to save the output directly to a file.
- **No Dependencies**: Requires only Node.js to run.

## Installation
1. Ensure you have Node.js installed on your system.
2. Clone this repository or download the script to your local machine.
3. Install the required dependencies by running `npm install` in the directory where the script is located.

## Usage
To use folder2sitemap, run the script from the command line, passing the path to the root directory of your website as an argument:

```bash
node folder2sitemap ./example.com
```

The script will output the structure of your website in JSON format to the console. You can redirect this output to a file if needed:

```bash
node folder2sitemap ./example.com > site_structure.json
```

### Saving Output to a File Directly
To save the output directly to a file, use the `--output` flag followed by the file name:

```bash
node folder2sitemap ./example.com --output site_structure.json
```
### Selecting Output Format
By default, the script outputs the website structure in JSON format. If you prefer to output the structure in CSV format, use the `--format=csv` flag:

```bash
node folder2sitemap ./example.com --format=csv
```

Would output the website structure in CSV format to the console. You can redirect this output to a file as well:

```csv
slug,title
"/","Home"
"/about/","About"
"/blog/","Blog"
"/blog/post1/","Post 1"
"/blog/post2/","Post 2"
```

### Excluding Directories

To exclude specific directories from the sitemap generation, use the `--exclude` flag followed by the directory name relative to the site root. You can specify multiple directories to exclude by using multiple `--exclude` flags. For example:

```bash
node folder2sitemap ./example.com --exclude=contentassets --exclude=zh-cn
```

This command will generate the sitemap without including the directories `/contentassets` and `/zh-cn`.

## Example Output
Given a website with a simple structure, the output might look like this:

```json
{
  "slug": "/",
  "title": "Home",
  "children": [
    {
      "slug": "/about/",
      "title": "About"
    },
    {
      "slug": "/blog/",
      "title": "Blog",
      "children": [
        {
          "slug": "/blog/post1/",
          "title": "Post 1"
        },
        {
          "slug": "/blog/post2/",
          "title": "Post 2"
        }
      ]
    }
  ]
}
```

## Visualizing the Sitemap
You can use online tools like [JSON Crack](https://jsoncrack.com/) to visualize the JSON output in a more structured format. Simply paste the JSON output into the tool to see a visual representation of the website structure.

![alt text](visual.png)
