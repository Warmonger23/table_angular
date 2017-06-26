<html>
   <head>
      <title>Machadalo</title>
      <script src = "https://ajax.googleapis.com/ajax/libs/angularjs/1.3.14/angular.min.js"></script>
      <style>
         table, th , td {
            border: 1px solid black;
            border-collapse: collapse;
            padding: 5px;
         }
         
         table tr:nth-child(odd) {
            background-color: #f2f2f2;
         }
         
         table tr:nth-child(even) {
            background-color: #ffffff;
         }
      </style>
      
   </head>
   
   <body >
   
      <h2>Sample Table</h2>
      <div ng-app = "mainApp" ng-controller = "studentController">
         <table id="t1">
            <tr>
            <th>Name</th>
            <th>Age</th>
            <th onclick="sort(2)">Gender</th>
            <th onclick="sort(3)">Marks in Hindi</th>
            <th onclick="sort(4)">Marks in English</th>
			<th> Average </th>
			<th> Total </th>
			<th> Delete </th>
            </tr>
            <tr ng-repeat = "subject in student.subjects">
                        <td>{{ subject.name }}</td>
                        <td>{{ subject.age }}</td>
                        <td>{{ subject.gender }}</td>
                        <td><div contenteditable="true" onfocus="sav(this)" onfocusout="test(this)">{{ subject.marksh }}</div></td>
                        <td><div contenteditable="true" onfocus="sav1(this)" onfocusout="test1(this)">{{ subject.markse }}</div></td>
						<td>{{ subject.markse/2+subject.marksh/2 }}</td>
						<td>{{ (subject.markse * 1) + (subject.marksh * 1)}}</td>
						<td><button onclick = "foo(this)"> Delete </button></td>
            </tr>
         </table>
		 <br><br>
		 <button onclick="fun(3)"> Get maximum in Hindi </button>		 <input type="text" id="ih" size="12"></input><br><br>
		 <button onclick="fun(4)"> Get maximum in English </button>		 <input type="text" id="ie" size="12"></input><br><br>
		 <button onclick="fun(5)"> Get maximum in Average </button>		 <input type="text" id="ia" size="12"></input><br><br>
      </div>
      <script type ="text/javascript">
         var mainApp = angular.module("mainApp", []);
         mainApp.controller('studentController', function($scope) {
            $scope.student = ({
               subjects:[
                  {name:'Ronit',age:'15',gender:'m',marksh:Math.floor(Math.random()*100+1),markse:Math.floor(Math.random()*100+1),id:'1'},
                  {name:'Usman',age:'16',gender:'m',marksh:Math.floor(Math.random()*100+1),markse:Math.floor(Math.random()*100+1),id:'2'},
                  {name:'Suhas',age:'15',gender:'m',marksh:Math.floor(Math.random()*100+1),markse:Math.floor(Math.random()*100+1),id:'3'},
                  {name:'Sumit',age:'15',gender:'m',marksh:Math.floor(Math.random()*100+1),markse:Math.floor(Math.random()*100+1),id:'4'},
                  {name:'Mohit',age:'15',gender:'m',marksh:Math.floor(Math.random()*100+1),markse:Math.floor(Math.random()*100+1),id:'5'},
                  {name:'Rahul',age:'14',gender:'m',marksh:Math.floor(Math.random()*100+1),markse:Math.floor(Math.random()*100+1),id:'6'},
                  {name:'Aditya',age:'15',gender:'m',marksh:Math.floor(Math.random()*100+1),markse:Math.floor(Math.random()*100+1),id:'7'},
                  {name:'Aditi',age:'16',gender:'f',marksh:Math.floor(Math.random()*100+1),markse:Math.floor(Math.random()*100+1),id:'8'},
                  {name:'Shubham',age:'15',gender:'m',marksh:Math.floor(Math.random()*100+1),markse:Math.floor(Math.random()*100+1),id:'9'},
                  {name:'Saurabh',age:'16',gender:'m',marksh:Math.floor(Math.random()*100+1),markse:Math.floor(Math.random()*100+1),id:'10'}
               ],
            });
         });
		 
		 function fill()
		 {
		 var table, rows, i, x, y;
		 console.log("sss");
            table = document.getElementById("t1");
			rows = table.getElementsByTagName("TR");
			var max=0;
			var ans="";
			var chk;
			for (i = 1; i < (rows.length); i++) {
				rows[i].getElementsByTagName("TD")[3].innerText= Math.floor(Math.random()*100+1);
				rows[i].getElementsByTagName("TD")[4].innerText= Math.floor(Math.random()*100+1);
				rows[i].getElementsByTagName("TD")[5].innerText=((rows[i].getElementsByTagName("TD")[3].innerText * 1)+(rows[i].getElementsByTagName("TD")[4].innerText * 1)) / 2;
				rows[i].getElementsByTagName("TD")[6].innerText=((rows[i].getElementsByTagName("TD")[3].innerText * 1)+(rows[i].getElementsByTagName("TD")[4].innerText * 1));
				}
				
		 }
		function fun(r) {
			var table, rows, i, x, y;
            table = document.getElementById("t1");
			rows = table.getElementsByTagName("TR");
			var max=0;
			var ans="";
			var chk;
			for (i = 1; i < (rows.length); i++) {
				var uu = (rows[i].getElementsByTagName("TD")[r].innerText);
				if (uu > max) {
					max = uu;
					ans = rows[i].getElementsByTagName("TD")[0].innerText;
				}
			}
			if (ans == "") ans = "Null";
			if(r==3)
			document.getElementById("ih").value=ans;
			else if (r==4)
			document.getElementById("ie").value=ans;
			else
			document.getElementById("ia").value=ans;
		}
		function foo(r) {
			var i = r.parentNode.parentNode.rowIndex;
			document.getElementById("t1").deleteRow(i);
		}
		var isme;
		function sav(r) {
			var txt = r.parentNode.parentNode.rowIndex;
			var table = document.getElementById("t1");
			var row   = table.getElementsByTagName("TR");
			isme = row[txt].getElementsByTagName("TD")[3].innerText;
		}
		function sav1(r) {
			var txt = r.parentNode.parentNode.rowIndex;
			var table = document.getElementById("t1");
			var row   = table.getElementsByTagName("TR");
			isme = row[txt].getElementsByTagName("TD")[4].innerText;
		}
		function test(r) {
		   var txt = r.parentNode.parentNode.rowIndex;
           var table = document.getElementById("t1");
		   var row   = table.getElementsByTagName("TR");
		   if(confirm("Do you want to save?"))
		   {
			  row[txt].getElementsByTagName("TD")[5].innerText=((row[txt].getElementsByTagName("TD")[3].innerText * 1)+(row[txt].getElementsByTagName("TD")[4].innerText * 1)) / 2;
			  row[txt].getElementsByTagName("TD")[6].innerText=((row[txt].getElementsByTagName("TD")[3].innerText * 1)+(row[txt].getElementsByTagName("TD")[4].innerText * 1));
			  
		   }
		   else{
			row[txt].getElementsByTagName("TD")[3].innerText=isme;
		   }
		}
		function test1(r) {
		   var txt = r.parentNode.parentNode.rowIndex;
           var table = document.getElementById("t1");
		   var row   = table.getElementsByTagName("TR");
		   if(confirm("Do you want to save?"))
		   {
			  row[txt].getElementsByTagName("TD")[5].innerText=((row[txt].getElementsByTagName("TD")[3].innerText * 1)+(row[txt].getElementsByTagName("TD")[4].innerText * 1)) / 2;
			  row[txt].getElementsByTagName("TD")[6].innerText=((row[txt].getElementsByTagName("TD")[3].innerText * 1)+(row[txt].getElementsByTagName("TD")[4].innerText * 1));
			  
		   }
		   else{
			row[txt].getElementsByTagName("TD")[4].innerText=isme;
		   }
		}
         function sort(n) {
             var table, rows, switching, i, x, y, shouldSwitch, dir, switchcount = 0;
             table = document.getElementById("t1");
             switching = true;
             dir = "desc";
				 while (switching) {
					switching = false;
					rows = table.getElementsByTagName("TR");
					for (i = 1; i < (rows.length - 1); i++) {
					  shouldSwitch = false;
					  x = rows[i].getElementsByTagName("TD")[n].innerText * 1;
					  y = rows[i + 1].getElementsByTagName("TD")[n].innerText * 1;
					  if(n==2)
					  {
					  if (rows[i].getElementsByTagName("TD")[n].innerText.toLowerCase() < rows[i+1].getElementsByTagName("TD")[n].innerText.toLowerCase()) {
						  shouldSwitch= true;
						  break;
						}
					  }
					  else
						{
						if (x < y) {
						  shouldSwitch= true;
						  break;
						}
						}
					}
					if (shouldSwitch) {
					  rows[i].parentNode.insertBefore(rows[i + 1], rows[i]);
					  switching = true;
					  switchcount++;      
					}
					
				}
         }
      </script>
   </body>
</html>
