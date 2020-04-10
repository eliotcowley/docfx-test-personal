---
uid: test-documentation-portal-index
title: Test Documentation Portal
_description: Homepage for the test documentation portal.
---

# Test Documentation Portal

This is a test documentation portal using DocFX, Markdown, and GitHub Actions to author and publish documentation with CI/CD.

## Install the tools

1. **DocFX**: This tool is used to build the documentation. Follow [Getting Started with DocFX](https://dotnet.github.io/docfx/tutorial/docfx_getting_started.html) to install DocFX. In step 2, I recommend downloading from GitHub.

2. [Git](https://git-scm.com/): Source control software that we use for the documentation. See this [Git cheat sheet](https://github.github.com/training-kit/downloads/github-git-cheat-sheet/) to get started.

3. [Visual Studio Code](https://code.visualstudio.com/): A lightweight code editor that we use for authoring docs in Markdown.

## Clone the documentation repository

1. Open **PowerShell**. 

2. Navigate to an easy-to-find location on your computer (like **C:\\**) using:
    ```powershell
    cd <location>
    ```

3. Enter the following command:
    ```powershell
    git clone https://github.com/eliotcowley/docfx-test-personal.git
    ```

## Build the docs site

> [!TIP]
> **Visual Studio Code** has a built-in terminal that you can use instead of opening a separate terminal window. Select **View > Terminal** to open it.

1. In **Powershell**, navigate to the docs repo folder using:
    ```powershell
    cd <location of folder>
    ```

2. Build the site with the following command:
    ```powershell
    docfx build -s
    ```

3. You should see some output, ending with the following:
    ```powershell
    Serving "<location of folder>\_site" on http://localhost:8080
    ```

4. In your web browser, navigate to **localhost:8080**. You should see the built documentation site running locally!

## Repository organization

The docs repository is organized as follows:

* The **articles** folder contains all of the documentation files (**.md** and **.yml**).
    * This folder is further organized into sub-folders corresponding to the top-level table of contents (**develop**, **publish**, **support**, **test**).
* The **images** folder contains all of the images for the documentation. This folder is organized the same way as **articles** to make it easy to find the images for a specific document.
* **docfx.json** contains settings for DocFX and should not be edited.
* **index.md** is the landing page for the documentation portal. All top-level pages also have a corresponding **index.md** file.
* **toc.yml** is the top-level table of contents. Each top-level category also has its own corresponding **toc.yml** file.
* Everything else is for DocFX and should not be edited.

## Learn Markdown

Markdown is the language used to author documents in the documentation portal. It is very similar to plain text and very easy to learn.

There are many flavors of Markdown, but the one we use is called [DocFX Flavored Markdown](https://dotnet.github.io/docfx/spec/docfx_flavored_markdown.html). DFM itself is built on top of [GitHub Flavored Markdown](https://guides.github.com/features/mastering-markdown/), so you can use any of the features of either flavor.

## Edit a document

1. Open **Visual Studio Code**.

2. Open the docs repo folder by selecting **File > Open Folder...** and browsing to the folder.

3. Find the document you want to edit. See [Repository organization](#repository-organization) to learn about the way the docs repository is organized so you can find what you're looking for.

4. Open the file to open it in Visual Studio Code's Markdown editor. (All documents are written in Markdown and have the **.md** file extension.) See [Learn Markdown](#learn-markdown) for more information on Markdown.

5. To preview the file, select the **Open Preview to the Side** icon in the top right (looks like two columns with a magnifying glass). Now you can edit the file and view its preview side-by-side.

6. Build the site locally by following the steps in [Build the docs site](#build-the-docs-site) to make sure it looks good.

## Add a new document

1. Open **Visual Studio Code**.

2. Open the docs repo folder by selecting **File > Open Folder...** and browsing to the folder.

3. Find the folder that should logically contain your new document. For example, if your new document will be under **Develop** in the TOC, then it should go in the **develop** folder.

4. Right-click the folder, select **New File**, and name the new file, giving it a **.md** extension. Our convention is to use all lowercase with hyphens in between words, and name the file the same as the title of the document.

5. Add a YAML header with metadata for the document. It must be at the top of the document and look like this:
    ```yaml
    ---
    uid: document-unique-id
    title: Title of Document
    _description: A brief description of the document.
    ---
    ```

    The YAML header contains the metadata for the document, which will go into the HTML `<head>` tag. The valid metadata are:
    * **uid**: A unique ID for the document, used for cross-referencing. Our convention is to use the filename, minus the **.md** extension.
    * **title**: The title of the document. This should match the H1 header.
    * **_description**: A brief description of the document.

6. Add an H1 header with a single `#` character. For example:
    ```markdown
    # Title
    ```

7. Write the rest of the document. If you need help with Markdown, see [Learn Markdown](#learn-markdown).

8. Add the document to the table of contents. TOC files are called **toc.yml**. You can find the relative TOC in the same folder as the document.

    TOC files are structured like this:

    ```yaml
    - name: Document1
      href: document1.md
    - name: Document2
      href: document2.md
      items:
        - name: Sub-Document
          href: sub-document.md
    ```

> [!NOTE]
> If you edit a TOC file, you may not see the changes reflected in a local build, even after refreshing the page. Try clearing your browser's cache and refreshing again if this happens.

## Publish your changes

Documentation is published to GitHub Pages every time you push to the `master` branch using **GitHub Actions**. Before you publish, make sure you build the docs locally by following the instructions in [Build the docs site](#build-the-docs-site).

Once you've built locally and you are good with the output, open the command line and push your changes.

1. Make sure you're on the `master` branch using `git status`.

2. Stage your changes:
    ```powershell
    git add .
    ```

3. Commit your changes with a message:
    ```powershell
    git commit -m "<Your message here>"
    ```

4. Push your changes:
    ```powershell
    git push
    ```

5. A push to `master` will kick off CI/CD, and your documentation will build and deploy to GitHub Pages automatically. This shouldn't take more than a few minutes. You can view progress on the [GitHub repo](https://github.com/eliotcowley/docfx-test-personal/actions).

6. Once the changes are deployed, you can view them on the [GitHub Pages website](https://eliotcowley.github.io/docfx-test-personal/).