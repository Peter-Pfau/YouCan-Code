# Read JSON File
## Node js Example

### Example
![image](https://github.com/user-attachments/assets/3c8a8cf9-07aa-41d4-8a68-a4ddcc595310)

### HTML
```HTML

```
### JavaScript

```JavaScript
<script>
// -------------------------------------------------------------- LOAD ----------------------------------------------------------------------------------
    const ReportDisplay = document.getElementById('ReportDiplayElementP');
    const theIPStackDelltb = document.getElementById('tbIPStackDell');
    const theTEMPIP = document.getElementById('tbTempIP')
    const theDayOuTb = document.getElementById('tbDayOU')

    async function domainControllerFetch() {
        const theDELLDC = document.getElementById('tbDELL').value;
        const theHPDC = document.getElementById('tbHP').value;
        // alert(theDELLDC)
        if(!theDELLDC){
            alert("Please enter a domain controller.");
        }
        else{
            const response = await fetch('https://vagwnopsalert1.va.gov/ActiveDirectory-view/WebPage/DCTransition/JSON/'+theDELLDC+'.json',{
            cache: 'no-cache',
            method: 'GET',
            headers: {
                    'Content-Type': "application/json; charset=UTF-8",
                    "Access-Control-Allow-Headers":"*",
                    "Access-Control-Allow-Origin":"*",
                    "Access-Control-Request-Headers":"authorization",
                    'Cache-Control': 'no-cache',
                    'Pragma': 'no-cache', // added for redundancy
                },
            
            });
            const json = await response.json();
            console.log(json); 
            // =========================== Servers ====================================
            let theHPDC = json.DC_HP;
            document.getElementById('tbHP').value  = theHPDC
            // ====================== Communications ==================================
            let theContactsCb = json.ContactsCb;
            if(theContactsCb === 'false'){document.getElementById('cbContacts').checked = false;} 
            if (theContactsCb === 'true') {document.getElementById('cbContacts').checked = true;}

            let theTransitionDate = json.TransitionDateTb;
            document.getElementById('tbTransitionDate').value = theTransitionDate
            let theAreaManager = json.AreaManagerTb;
            document.getElementById('tbAreaManager').value = theAreaManager
            let theOpsManager = json.OpsManagerTb;
            document.getElementById('tbOpsManager').value = theOpsManager
            let theSiteContact = json.SiteContactTb;
            document.getElementById('tbSiteContact').value = theSiteContact
            let theLANContact= json.LANContactTb;
            document.getElementById('tbLANContact').value = theLANContact

            let theEmailInitialCommunication = json.EmailInitialCommunicationCb;
            if(theEmailInitialCommunication === 'false'){document.getElementById('cbEmailInitialCommunication').checked = false;} 
            if (theEmailInitialCommunication === 'true') {document.getElementById('cbEmailInitialCommunication').checked = true;}

            let theMeetingInvite = json.MeetingInviteCb;
            if(theMeetingInvite === 'false'){document.getElementById('cbMeetingInvite').checked = false;} 
            if (theMeetingInvite === 'true') {document.getElementById('cbMeetingInvite').checked = true;}

            let theEmailSuspendMonitor = json.EmailSuspendMonitorCb;
            if(theEmailSuspendMonitor === 'false'){document.getElementById('cbEmailSuspendMonitor').checked = false;} 
            if (theEmailSuspendMonitor === 'true') {document.getElementById('cbEmailSuspendMonitor').checked = true;}

            let theLEAFRequest = json.LEAFRequestCb;
            if(theLEAFRequest === 'false'){document.getElementById('cbLEAFRequest').checked = false;} 
            if (theLEAFRequest === 'true') {document.getElementById('cbLEAFRequest').checked = true;}

            // ======================= Change Control ================================

            let theChangeOrder = json.ChangeOrderTb;
            document.getElementById('tbChangeOrder').value = theChangeOrder
            
            let theLANSupportRequest = json.LANSupportRequestTb;
            document.getElementById('tbLANSupportRequest').value = theLANSupportRequest
            
            let theDecomRequest = json.DecomRequestTb;
            document.getElementById('tbDecomRequest').value = theDecomRequest
            

            // =================== Configuration Checks ==============================

            let theFSMORolescb = json.FSMORolesCb;
            let theFSMORolesTa = json.FSMORolesTa;
            // Get the textarea From JSON file and replace <br>  with  \n
            const theFSMORolesTaNoBR = theFSMORolesTa.replace(/<br>/g, "\n"); 
            document.getElementById('taFSMORoles').value = theFSMORolesTaNoBR
            if(theFSMORolescb === 'false'){document.getElementById('cbFSMORoles').checked = false;} 
            if (theFSMORolescb === 'true') {document.getElementById('cbFSMORoles').checked = true;}

            // const theDELLDC = document.getElementById('tbDELL').value;
            let theArray = theDELLDC.split(".");
            let theDomain = theArray.slice(1).join(".");
            document.getElementById('codeFSMORoles').innerText = "Get-ADDomain " + theDomain + " | Select-Object InfrastructureMaster, RIDMaster, PDCEmulator" + "\n" +
            "Get-ADForest " + theDomain + " | Format-Table SchemaMaster, DomainNamingMaster"

            let theIPStackDellcb = json.IPStackDellcb;
            let theIPStackDellTa = json.IPStackDellTa;
            const theIPStackDellTaNoBR = theIPStackDellTa.replace(/<br>/g, "\n"); 
            document.getElementById('taIPStackDell').value = theIPStackDellTaNoBR
            if(theIPStackDellcb === 'false'){document.getElementById('cbIPStackDell').checked = false;} 
            if (theIPStackDellcb === 'true') {document.getElementById('cbIPStackDell').checked = true;}
            document.getElementById('codeIPConfig').innerText = "    enter-pssession " + theDELLDC + " \n " + "   ipconfg /all"

            let theTempIPcb = json.TEMPIPcb;
            if(theTempIPcb === 'false'){document.getElementById('cbTempIP').checked = false;} 
            if (theTempIPcb === 'true') {document.getElementById('cbTempIP').checked = true;}
            theTEMPIP.value = json.TEMPIPtb

            let theDayOUcb = json.DayOUcb;
            if(theDayOUcb === 'false'){document.getElementById('cbDayOU').checked = false;} 
            if (theDayOUcb === 'true') {document.getElementById('cbDayOU').checked = true;}
            theDayOuTb.value = json.DayOuTb;

            let theDecryptDrivesDellCb = json.DecryptDrivesDellCb;
            if(theDecryptDrivesDellCb === 'false'){document.getElementById('cbDecryptDrivesDell').checked = false;} 
            if (theDecryptDrivesDellCb === 'true') {document.getElementById('cbDecryptDrivesDell').checked = true;}

            let theTempConnectionsCb = json.TempConnectionsCb;
            if(theTempConnectionsCb === 'false'){document.getElementById('cbTempConnections').checked = false;} 
            if (theTempConnectionsCb === 'true') {document.getElementById('cbTempConnections').checked = true;}
            document.getElementById('codeTempConnections').innerText = "    (Get-ADDomainController -filter * -Server " + theDomain + ").Hostname "

            let theDCHealthCb = json.DCHealthCb;
            if(theDCHealthCb === 'false'){document.getElementById('cbDCHealth').checked = false;} 
            if (theDCHealthCb === 'true') {document.getElementById('cbDCHealth').checked = true;}
            document.getElementById('codeDCHealth').innerText = "    \"" +theDELLDC+"\" | q:\\Get-DCHealth.ps1 -email -to peter.pfau@va.gov \n"+
            "    \""+theHPDC+ "\" | q:\\Get-DCHealth.ps1 -email -to peter.pfau@va.gov "

            let theRemoteManagementCb = json.RemoteManagementCb;
            if(theRemoteManagementCb === 'false'){document.getElementById('cbRemoteManagement').checked = false;} 
            if (theRemoteManagementCb === 'true') {document.getElementById('cbRemoteManagement').checked = true;}

            theHostname = theArray[0];
            document.getElementById('codeRemoteManagement').innerText = "    Dell DC: Connect to target server via iDRAC... http://iDRAC-"+theHostname+".rmoc.va.gov \n\n"+
            "    HP DC: Connect to HP Oneview for new HP... https://vagwnapphpdc01/#/login"

            let theEmailResumedMonitor = json.EmailResumeMonitorCb;
            if(theEmailResumedMonitor === 'false'){document.getElementById('cbEmailResumeMonitor').checked = false;} 
            if (theEmailResumedMonitor === 'true') {document.getElementById('cbEmailResumeMonitor').checked = true;}


            fireChangeEvent(); 

        }
    }

    btnLoad.addEventListener('click',domainControllerFetch);
</script>

```
