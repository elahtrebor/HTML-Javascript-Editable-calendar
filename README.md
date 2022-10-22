# HTML-Javascript-Editable-calendar
Editable calendar done in pure vanilla Javascript

<html>

<script>
function seq (start, end){
 var i;
 var arr = new Array();
 for(i = start;i <= end; i++){
   arr.push(i);
  }
 return arr;
}


function intToDayOfWeek(num){
var daysOfWeek = ["Sunday", "Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday"];
return daysOfWeek[num];
}

function monthToString(month){
var months = [ "01", "02", "03", "04", "05", "06", "07", "08", "09", "10", "11", "12" ];
 return months[month]; 
}

function monthName(month){
var months = [ "January", "February", "March", "April", "May", "June", "July", "August", "September", "October", "November", "December" ];
 return months[month]; 
}

function getCurrentYear(){
 return new Date().getFullYear();
}

function getDaysInMonth(year, month) {
 month = parseInt(month) + 1; 
 //alert("year: " + year + " month: " + month);
  return new Date(year, month, 0).getDate();
}

function print(str){
 document.write(str);
}

function dbg(str){
document.getElementById('debug1').value = str;
}

function drawMonth(month){
// Months start at 0 - 11
// Days of week are 0 - 6 where monday is the first day
 var year = getCurrentYear();
 var numOfDays = getDaysInMonth(year, month);
 //var datestr = year + "-" + monthToString(month) + "-" + "01";
 var datestr = monthName(month) + " 1, " + year + " 00:00:00";
 var dow = new Date(datestr).getDay();
  print("<center><h3>" + monthName(month) + "</h3><br>");
 // print the table header
 print("<table border = 1; style='border-collapse: collapse'>\n"); 
 print("<tr style='background: lightgray'><th >Sunday</th><th>Monday</th><th>Tuesday</th><th>Wednesday</th><th>Thursday</th><th>Friday</th><th>Saturday</th></tr>"); 
 // print the empty days first then print the rest iterating through the last day of the month
 // keep a row count and if is equal to 6 then print a new row
  print("<tr>");
  var count = 1;
  var colcount = 0;
 // start looping over the first part 
 for(var i = 0; i <= dow; i++){
  // if the current column is less than the start day then just print empty spaces 
  if(colcount <  dow) { 
       print("<td contenteditable='true' >&nbsp</td>");  
   }
   else { 
      // otherwise print the day number in the cell
     print("<td contenteditable='true'>" + count + "</td>"); 
     count++;
        }
     // reset the rowcount 
      if(colcount == 6) { 
       print("</tr>\n");
       colcount = 0; 
       }
      else {
        colcount++;
        }
  }


    //  This finishes the rest of the calendar
   for(i = count; i<=numOfDays;i++){
       print("<td contenteditable='true'>" + count + "</td>");
     
       if(colcount == 6) { 
             print("</tr>\n");
             colcount = 0;
         } 
        else { 
                colcount++;
          }

        count++; 
   }

// alert(month + " " + numOfDays + " " + year );

 print("</table><br>\n");
// print("<button onclick='location.reload();'>back</button>");
 //print("<div><hr></div>\n");
} // END drawMonth()


function drawCal(){
var months = seq(0,11);
 for(var i = 0; i < months.length;i++){
  drawMonth(i); 
 }


}

</script>
<body onload= "drawCal()">
</html>
