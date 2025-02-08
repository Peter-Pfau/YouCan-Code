# Fetch - JSON File
## Node js Example

### Example
![image](https://github.com/user-attachments/assets/a8a323d4-bee2-4932-bc9b-6b64668caf24)


### HTML
```HTML
    <div class="box">
        <div class="input-with-image">
            <input type="text" id="tbDELL" value="VHAMPI3DC1.mpi.v21.med.va.gov" >
            <img id="downArrowSelect" src="../Images/downArrowSelect.svg">
        </div>
    </div>
```
### JavaScript
```JavaScript

<script>
    const imgDownArrowSelectDC = document.getElementById('downArrowSelect');

    imgDownArrowSelectDC.addEventListener('click',() =>{
        getDomainControllers();
        modalSelectDC.style.display = 'block';
    })
    async function getDomainControllers() {
    const response = await fetch('https://vagwnopsalert1.va.gov/ActiveDirectory-view/Reports/DomainControllerList.JSON',{
            method: 'GET',
            headers: {
                    'Content-Type': "application/json; charset=UTF-8",
                    "Access-Control-Allow-Headers":"*",
                    "Access-Control-Allow-Origin":"*",
                    "Access-Control-Request-Headers":"authorization"
                }
            });
        const json = await response.json();
        console.log(json); 
        var Array = json
        //alert(Array[0].HostName)
        var myFirstDC = Array[0].Domain
        let length =  Array.length;
        var selectElementFunction = document.getElementById("selectModalDC");
        // alert(selectElementFunction.value);
        // Loop through the options array and create option elements
        selectElementFunction.innerHTML = ""; // Remove existing options
        for (var i = 0; i < Array.length; i++) {
                    var option = document.createElement("option");
                    option.value = Array[i].HostName;
                    option.text = Array[i].HostName;
                    selectElementFunction.appendChild(option);
        }
    }
</script>
```
