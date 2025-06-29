## BucketLoot - S3 BUCKET DUMP
---
> Enumerate **every** object path in a **public S3 bucket** and print or save full **URLs**.

BucketLoot is a **lightweight**, **parallelized** Python tool for **listing** the contents of **public S3 buckets**, optionally filtering by file extension (`dump-type`), and even uploading files via PUT.

---

### 🔍 Key Features

* **Object Listing**: Automatically handles pagination (`ContinuationToken`) for buckets with thousands of objects.
* **Parallel Requests**: Uses `ThreadPoolExecutor` with a default of 20 workers to speed up bucket listing.
* **Extension Filter**: Optionally include only keys ending with a specific file extension (e.g., `.pdf`, `.txt`).
* **Upload Support (`--put`)**: Upload a local file to the bucket via HTTP PUT if permissions allow.
* **Colored Logging**: Uses ANSI escape codes to colorize INFO, DEBUG, and ERROR messages.
* **Loading Animation**: Displays a live spinner and rotating messages while listing objects.
* **Verbose Mode**: Enable detailed debugging output with `-v`.
* **Credits**: Show tool credits and author contacts with `--credits`.

---

### 🚀 Installation

1. Clone this repository:

   ```bash
   git clone https://github.com/Snillx/BucketLoot.git
   cd BucketLoot
   ```

2. (Optional) Create and activate a virtual environment:

   ```bash
   python3 -m venv .venv
   source .venv/bin/activate
   ```

3. Install dependencies:

   ```bash
   pip install -r requirements.txt
   ```

> **Requirements:** Python 3.7+, `requests`

---

### ⚙️ Usage

```bash
python bucketloot.py -u <BUCKET_URL> [options]
```

You can also

#### Command-Line Arguments

| Flag              | Description                                                                 |
| ----------------- | --------------------------------------------------------------------------- |
| `-u`, `--url`     | **(Required)** Base bucket URL (e.g., `https://mybucket.s3.amazonaws.com`). |
| `--dump-type`     | Include only keys that end with this extension (e.g., `pdf`, `txt`).        |
| `-o`, `--output`  | Write output to a file instead of printing to stdout.                       |
| `-v`, `--verbose` | Enable verbose (DEBUG) logging.                                             |
| `--put <file>`    | Upload a local `<file>` to the bucket via HTTP PUT.                         |
| `--credits`       | Display author credits and contact info, then exit.                         |

#### Examples

* List all objects and print URLs:

  ```bash
  python bucketloot.py -u https://mybucket.s3.amazonaws.com
  ```

* Filter only `.txt` files and save to `list.txt`:

  ```bash
  python bucketloot.py -u https://mybucket.s3.amazonaws.com --dump-type txt -o list.txt
  ```

* Upload a file to the bucket:

  ```bash
  python bucketloot.py -u https://mybucket.s3.amazonaws.com --put archive.zip
  ```

---

### 🛠️ Internal Implementation

* **`BucketLoot._fetch_and_parse_page`**: Sends paginated GET requests and parses the XML for `<Key>` elements.
* **Thread Pool**: Defaults to 20 threads in `ThreadPoolExecutor` for concurrent page fetches.
* **Colorful Logger**: ANSI-based `ColoredFormatter` for stderr logs, with INFO/DEBUG in yellow and ERROR/CRITICAL in red.
* **Loading Animation**: `loading_animation()` shows rotating messages (`"Gathering files..."`, etc.) until the first page fetch.
* **Upload Logic**: Uses `requests.put()` to perform the PUT operation and parses S3 XML error responses when present.

---

### 🤝 Contributing

1. Fork the repository
2. Create a feature branch: `git checkout -b feature/fooBar`
3. Commit your changes: `git commit -m 'Add awesome feature'`
4. Push to the branch: `git push origin feature/fooBar`
5. Open a Pull Request

---

### 📄 License

This project is licensed under the [MIT License](LICENSE).

---

> **Author:** Snillx ([https://github.com/Snillx](https://github.com/Snillx))


