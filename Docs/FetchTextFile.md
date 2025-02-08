# Fetch Text File
# Node JS Example

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
