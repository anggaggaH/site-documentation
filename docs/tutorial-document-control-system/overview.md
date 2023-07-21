---
sidebar_position: 0
---

# Overview
Document Control System
- PHP Version : 7.2 or should less than 7.3
- Codeigniter Version: 3.1.9
- Cloud : [Azure Storage](https://github.com/Azure/azure-sdk-for-php)
- Azure Storage Explorer : [Install](https://azure.microsoft.com/en-us/products/storage/storage-explorer/)

## Dashboard
<img src="/img/docs/overview/1. dashboard.png" alt="dashboard" />
Description: Showing all product categories

## Header
<img src="/img/docs/overview/2. header.png" alt="header" />
Description:
<ol type="1">
 <li>Navigation menu</li>
 <li>Add new project</li>
 <li>Dashboard</li>
 <li>Edit project *</li>
 <li>Copy project*</li>
 <li>Delete project*</li>
 <li>Share project*</li>
</ol>
note:
<ol type="a">
    <li><b>*</b> active on project detail page.</li>
    <li>Copy project will create new project based on current project (will be redirected to Create New Page).</li>
    <li>Share function never works from beginning.</li>
</ol>

## Menu
<img src="/img/docs/overview/3. menu.png" alt="menu" />

note: * some features still have issues after migrating to azure storage

## Home
<img src="/img/docs/overview/4. home.png" alt="home" />
Description: Showing data based on the category that we choose from the dashboard


## Create-Update Project
<img src="/img/docs/overview/5. create-update.png" alt="create-update" />
Description:
<ol type="1">
 <li>We can turn off the validation for filename format on this <a href="https://docs.bdsamferdsel.no/Project/Code" target="_blank" alt="">page</a> so that the filename can be anything but remember this validation format can prevent the user from uploading the same filename on different.</li>
 <li>Before doing an upload the file will be checked whether:</li>
 a. the filename format was correct
 <br/>
 b. the file is exist or not in our storage (if the file is exist file can be replaced or not)
 <br/>
 c. and it will be stored on our database after upload to storage is success

 <li>File with <b>Private</b> will be stored in the Private Container and public files will be stored in the public container</li>
 <li>On edit mode changing private-public will move file from source to target container</li>
</ol>

## Project Detail
<img src="/img/docs/overview/6. project detail.png" alt="project detail" />
note: * need to refactor the function that shows the relations


