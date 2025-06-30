

# Asset Management Portal

This project implements an Asset Management Portal built on the **ServiceNow platform**, leveraging its core functionalities for data management, process automation, and user interface customization.

## Core Components

### 1\. Table Definition: `asset inventory`

  * [cite\_start]**Platform Feature**: Custom Table [cite: 14]
  * [cite\_start]**Label**: `asset inventory` [cite: 20]
  * [cite\_start]**Name (Internal)**: `u_asset_inventory` [cite: 21]
  * **Purpose**: Stores all asset records, acting as the primary data model for the application. [cite\_start]Each record in this table corresponds to a database row, and each field to a column[cite: 18].
  * **Key Columns (Fields)**:
      * [cite\_start]`purchase date`: `Date` type, Max length: `40` [cite: 26]
      * [cite\_start]`warranty expire`: `Date` type, Max length: `40` [cite: 26]
      * [cite\_start]`Sys ID`: `Sys ID (GUID)` type, Max length: `32` [cite: 26]

### 2\. Security & Access Control: Access Controls (ACLs)

  * [cite\_start]**Platform Feature**: Access Control List (ACL) Rules [cite: 65, 73]
  * [cite\_start]**Target Table**: `u_asset_inventory` [cite: 75]
  * [cite\_start]**Decision Type**: `Allow If` [cite: 75]
  * **Operations Configured**:
      * [cite\_start]`write`: `true` (active) [cite: 75]
      * [cite\_start]`read`: `true` (active) [cite: 75]
      * [cite\_start]`delete`: `true` (active) [cite: 75]
      * [cite\_start]`create`: `true` (active) [cite: 75]
  * [cite\_start]**Managed by**: `admin` user [cite: 75]
  * [cite\_start]**Last Updated**: 2025-06-28 20:40:18 [cite: 75]

### 3\. User Interface Enhancements: UI Actions

  * [cite\_start]**Platform Feature**: UI Actions [cite: 93, 105, 154, 205, 259]
  * **Purpose**: Provide interactive buttons and links on forms to trigger server-side or client-side logic.
  * **Implemented Actions**:
      * **`mark as lost`**:
          * [cite\_start]**Type**: Form button [cite: 111]
          * [cite\_start]**Action Name**: `mark_as_lost` [cite: 116]
          * [cite\_start]**Condition Script**: `current.u_status!='lost'` [cite: 162]
          * [cite\_start]**Server-side Script (JavaScript)**: [cite: 163]
            ```javascript
            current.u_status='lost'; [cite_start]// Sets the 'u_status' field of the current record to 'lost' [cite: 174]
            current.update(); [cite_start]// Persists the changes to the database [cite: 177]
            action.setRedirectURL(current); [cite_start]// Redirects the user back to the current record [cite: 180]
            ```
      * **`mark as repaired`**:
          * [cite\_start]**Type**: Form button [cite: 219]
          * [cite\_start]**Action Name**: `mark_as_repaired` [cite: 223]
          * [cite\_start]**Auto-created records**: `UX Form Action` and `UX Form Action Layout Item` records [cite: 210]
      * **`mark as damaged`**:
          * [cite\_start]**Type**: Form button [cite: 273]
          * [cite\_start]**Action Name**: `mark_as_damaged` [cite: 278]
          * [cite\_start]**Auto-created records**: `UX Form Action` and `UX Form Action Layout Item` records [cite: 264]

### 4\. Automation & Scheduled Tasks: Scheduled Script Execution

  * [cite\_start]**Platform Feature**: Scheduled Jobs / Scheduled Script Execution [cite: 314]
  * [cite\_start]**Name**: `warranty expiry alert` [cite: 318]
  * [cite\_start]**Frequency**: `Daily` [cite: 328]
  * [cite\_start]**Execution Time**: 12:00:00 [cite: 331, 332, 333]
  * [cite\_start]**Script (JavaScript)**: [cite: 334]
    ```javascript
    var grAsset = new GlideRecord('u_asset_inventory'); [cite_start]// Instantiates a GlideRecord object for the u_asset_inventory table [cite: 338]
    var today = new GlideDateTime(); [cite_start]// Instantiates a GlideDateTime object for the current date and time [cite: 341]
    // Further logic would be implemented here to check warranty expiry and trigger alerts/notifications.
    ```
  * [cite\_start]**Scripting Environment**: ECMAScript 2021 (ES12) mode can be turned on for this script[cite: 335].

### 5\. Reporting & Analytics: Report Generation

  * [cite\_start]**Platform Feature**: Reporting Module [cite: 353, 360]
  * [cite\_start]**Report Title**: `available vs assigned assets` [cite: 369]
  * [cite\_start]**Source Table**: `asset inventory` (`u_asset_inventory`) [cite: 375]
  * **Configuration Options**:
      * [cite\_start]Display data labels [cite: 377]
      * [cite\_start]Chart size: `Large` [cite: 385]
      * [cite\_start]Decimal precision: `2` [cite: 393]
      * [cite\_start]Supports adding conditions for data filtering [cite: 386]

### 6\. Data Presentation: List View

  * [cite\_start]**Platform Feature**: List View [cite: 411, 418]
  * [cite\_start]**Target Table**: `u_asset_inventory` [cite: 413]
  * **Purpose**: Provides a tabular display of records from the `asset inventory` table, enabling searching and quick overview of data.
  * [cite\_start]**Displayed Columns**: `number`, `Asset name`, `assigned to`, `purchase date`, `Status`, `Sys ID`, `warranty expire` [cite: 424, 427, 433, 434, 435, 436, 449]
