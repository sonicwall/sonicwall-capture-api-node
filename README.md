# Steps to use the module in node backend project.

## 1. Install
        npm install --save https://github.com/sonicwall/sonicwall-capture-api-node.git

## 2. Include
        var captureApi = require('capture-api');
        
## 3. Syntax
+ 3.1 Build http request options object.
    ```
        const httpOptions = {
          hostname: string,   // Required.
          sn: stirng,         // Required for auth.
          key: stirng         // Required for auth.
        };
    ```
        
+ 3.2 list method.
    ```
        const listObj = {
          before: number,     // Optional. Unix timestamp.
          after: number,      // Optional. Unix timestamp.
          pageSize: number,   // Optional.
          pageIndex: number,  // Optional.
        };
        captureApi.list(httpOptions, listObj).then(result => {
          console.log(result);
        }).catch(ex => { });
    ```

+ 3.3 report method.
    ```
        const reportObj = {
          resource: string,   // Required. md5/sha1/sha256/scan_id
          allInfo: boolean    // Optional. If return additional information about the file. Default is false.
        }
        captureApi.report(httpOptions, reportObj).then(result => {
          console.log(result);
        }).catch(ex => { });
    ```

+ 3.4 artifact method.
    ```
        const artifactSha256: string; // Required.
        captureApi.artifact(httpOptions, artifactSha256).then(result => {
          console.log(result);
        }).catch(ex => { });
    ```
        
+ 3.5 scan method.
    ```
        const scanFilePath: string; // Required.
        captureApi.scan(httpOptions, scanFilePath).then(result => {
          console.log(result);
        }).catch(ex => { });
    ```

+ 3.6 download method.
    ```
        const downloadObj = {
          sha256: string,                          // Required.
          engine: string,                          // Required.
          env: string,                             // Required.
          type: "report" | "pcap" | "screenshots", // Required.
          filePath: string                         // Required. File will be saved there.
        }
        captureApi.download(httpOptions, downloadObj).then(result => {
          console.log(result);
        }).catch(ex => { });
    ```

# Steps to use command line tool. Please see last section for param type.
## 1. Global Install
    sudo npm install --global https://github.com/sonicwall/sonicwall-capture-api-node.git
        
## 2. Syntax
+ 2.1 list
    ```
    // List by default list params.
    capture-api-cli -hostname <required> -sn <required> -key <required> -list
    
    // List by custom list params.
    capture-api-cli -hostname <required> -sn <required> -key <required> -list-before <optional> -list-after <optional> -list-page-size <optional> -list-page-index <optional>
    ```

+ 2.2 report
    ```
    capture-api-cli -hostname <required> -sn <required> -key <required> -report-resource <required> -report-all-info <optional 1 or 0>
    ```

+ 2.3 artifact
    ```
    capture-api-cli -hostname <required> -sn <required> -key <required> -artifact-sha256 <required>
    ```

+ 2.4 scan
    ```
    capture-api-cli -hostname <required> -sn <required> -key <required> -scan-file-path <required>
    ```

+ 2.5 download
    ```
    capture-api-cli -hostname <required> -sn <required> -key <required> -download-sha256 <required> -download-engine <required> -download-env <required> -download-type <required> -download-file-path <required>
    ```

