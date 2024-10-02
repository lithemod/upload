# Upload

A simple PHP module for handling file uploads with ease.

## Installation

You can easily install the Upload module using Composer. Run the following command:

```bash
composer require lithemod/upload
```

## Usage

Here's a basic example of how to use the `Upload` module after installation:

1. **Handling File Uploads:**
   Create an HTML form for file uploads:

   ```html
   <form action="upload.php" method="post" enctype="multipart/form-data">
       <input type="file" name="fileToUpload" />
       <input type="submit" value="Upload" />
   </form>
   ```

2. **Processing the Upload:**
   In your `upload.php`, use the `Upload` class to handle the file:

   ```php
   <?php

   require 'vendor/autoload.php'; // Include Composer's autoloader

   use Lithe\Base\Upload;

   if ($_SERVER['REQUEST_METHOD'] === 'POST') {
       // Create an instance of the Upload class with the uploaded file
       $upload = new Upload($_FILES['fileToUpload']);

       // Specify the upload directory and allowed extensions
       $uploadDir = 'uploads';
       $allowedExtensions = ['jpg', 'png', 'gif', 'txt'];

       // Move the uploaded file
       $filePath = $upload->move($uploadDir, $allowedExtensions);

       if ($filePath) {
           echo "File uploaded successfully: $filePath";
       } else {
           echo "File upload failed.";
       }
   }
   ```

## Methods

### `__construct(array $file)`

- Initializes the upload instance with the file data.

### `move(string $uploadDir, ?array $allowedExtensions = null): ?string`

- Moves the uploaded file to the specified directory.
- Generates a unique filename to avoid overwriting.
- Optionally validates the file extension against allowed extensions.

### `isUploaded(): bool`

- Checks if a file is successfully uploaded.

### `getMimeType(): ?string`

- Retrieves the MIME type of the uploaded file.

### `getSize(): ?int`

- Retrieves the size of the uploaded file in bytes.

## Error Handling

The module throws exceptions for various error scenarios, including:

- Invalid file upload array
- Upload directory does not exist or is not writable
- File extension not allowed

Make sure to wrap the usage of the module in try-catch blocks to handle exceptions appropriately.

```php
try {
    // Upload handling code
} catch (Exception $e) {
    echo 'Error: ' . $e->getMessage();
}
```

## License

This module is licensed under the MIT License. See the [LICENSE](LICENSE) file for more information.