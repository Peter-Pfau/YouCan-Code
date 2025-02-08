# Fetch - Text File
# Node js Example

### Example
![image](https://github.com/user-attachments/assets/048b3d52-f5f4-4144-bb10-732902a24199)



### HTML
``` HTML
        <input type="checkbox" id="cbIPStackDell" name="cbIPStackDell" value="">IPConfig from the old Dell hardware. 
        <span style="padding-right:3px; padding-top: 3px; display:inline-block;">
            <img id="iIPConfig" class="manImg" src="../images/nic.jpg" style="cursor: pointer;" width=100 height=100></img>               
            </span>
        <!-- <span id="sIPConfig" style="cursor: pointer;"><font size=16></font></span>  -->
        <br><br>
        <textarea id="taIPStackDell" rows="7" cols="100" value=""></textarea>  
```

### JavaScript
```PowerShell
<script>
    function stripNonPrintableAndNormalize(text) {
        text = text.replace(/[^\x20-\x7F]/g, '');
        // strip control chars
        text = text.replace(/\p{C}/gu, '');
        // other common tasks are to normalize newlines and other whitespace
        // normalize newline
        text = text.replace(/\n\r/g, '\n');
        text = text.replace(/\p{Zl}/gu, '\n');
        text = text.replace(/\p{Zp}/gu, '\n');
        // normalize space
        text = text.replace(/\p{Zs}/gu, ' ');
        return text;
    }
    async function getIPConfig() {
                alert("Getting IPConfig "+theDomain+ " ...")
                const response = await fetch('Reports/IPConfig/VAC103DC1V23.v23.med.va.gov.IPConfig.txt', {
                    method: 'GET',
                    headers: {
                        'Content-Type': "text/html; charset=UTF-8",
                        "Access-Control-Allow-Headers":"*",
                        "Access-Control-Allow-Origin":"*",
                        "Access-Control-Request-Headers":"authorization"
                    },
                });
                const result = await response.text();
                console.log ("Success:", result)
                const theText = stripNonPrintableAndNormalize(result)

                console.log ("Success:",  theText )
                document.getElementById('taIPStackDell').value = theText;    
    }
    const imgElement = document.getElementById('iIPConfig')
    imgElement.addEventListener('click',getIPConfig);
</script>
```
