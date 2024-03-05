# Hilanet-Script
This is a fork of a repo written by GuyHassan and adjusted for GM parameters.
In order for it to work you'll need to:
1. Change Hilan language to english.
2. Be at the end of the month (have a red 'x') by all the relevant days.
3. Go to left hamburger menu -> attendence -> reports -> report & update
4. Select 'Errors'
5. Follow the below instructions to fill in the relevant days.

To start, go to the orginizational Hilan sign in day
```https://gm.net.hilan.co.il/login```

```
const entryTime = '09.00';
const exitTime = '18.30';

const convertFloatToTime = (num) => num.replace('.', ':');

document.querySelectorAll("input[name*='ManualEntry_EmployeeReports_row']").forEach((item) => {
    item.value = convertFloatToTime(entryTime);
});

document.querySelectorAll("input[name*='ManualExit_EmployeeReports_row']").forEach((item, idx) => {
    const totalCell = document.querySelectorAll('.ROC.gridRowStyle.ItemCell, .ROC.alternateRowStyle.ItemCell')[2 + idx * 3];
    
    item.value = convertFloatToTime(exitTime);
    const splitedNumber = (exitTime - entryTime).toFixed(2).split('.')
    const calcNumber = `${splitedNumber[0].padStart(2, '0')}.${splitedNumber[1]}`;
    totalCell.innerHTML = convertFloatToTime(calcNumber);
});


Array.from(document.getElementsByClassName(' regularItemCell ItemBorder')).forEach((item, idx) => {
    const dateCell = item.getAttribute('ov');

    if (dateCell.includes('Mon') || dateCell.includes('Wed')) {
        document.querySelectorAll("select[name*='SymbolId_EmployeeReports_row']")[idx].value = '100';
    } else {
        document.querySelectorAll("select[name*='SymbolId_EmployeeReports_row']")[idx].value = '0';
    }
});
```
when you get this page, you need to select all of your days that with the **red x sign** (days you did not mark working hours), after you select all your days click on the **Sel. Days** button

![image](https://github.com/GuyHassan/Hilanet-Script/assets/33221427/34e5902f-d708-4cd2-9fea-c752df225f41)

now all your days is move to the table

![image](https://github.com/GuyHassan/Hilanet-Script/assets/33221427/bab72735-9a5b-43d5-b9d7-e1c75a1b32c3)

open the **Inspect** and go to Sources, open new Snippet and call it whatever you want (i call it **Hilan**)
paste the code inside the file and click on the Hilan tab right click and click on Run button.

![image](https://github.com/GuyHassan/Hilanet-Script/assets/33221427/34a9fdf4-3c87-4a0f-8726-46ff39e03a8a)

now your rows is filled automatically.

