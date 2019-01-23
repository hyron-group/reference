## **Table of contents**

### interface **HyronService**

Used to declare service metadata declare about a group of router that could be used to listen on specified port

-   *static* **requestConfig** ( ) : RouterMeta

### interface **RouterMeta**

-   **method**: SupportedMethod | Array<SupportedMethod>;
-   **fontware**: Array<string>;
-   **backware**: Array<string>;
-   **plugins**: Array<string>;
-   **handle**: mainExecuter;
-   **path**: string;
-   **params**: string;

## **Details**

