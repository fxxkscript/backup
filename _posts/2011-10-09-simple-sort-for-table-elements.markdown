---
layout: post
title: !binary |-
  566A5piT55qE6KGo5qC85o6S5bqP
wordpress_id: 116
wordpress_url: !binary |-
  aHR0cDovL3JheWNuLm5ldC8/cD0xMTY=
date: 2011-10-09 09:07:19.000000000 +08:00
---
[javascript]
	function sortrows(table,n) {
		//first &lt;tbody&gt;
		var tbody = table.tBodies[0];
		var rows = tbody.getElementsByTagName('tr');
		//convert NodeList to Array
		rows = Array.prototype.slice.call(rows,0);
		
		rows.sort(function(row1,row2) {
			var cell1 = row1.getElementsByTagName('td')[n];
			var cell2 = row2.getElementsByTagName('td')[n];
			var var1 = cell1.textContent || cell1.innerText;
			var var2 = cell2.textContent || cell2.innerText;
			var1 = var1 - 0;
			var2 = var2 - 0;
			if(var1 &gt; var2) {
				return 1;
			} 
			else if(var1 &lt; var2) {
				return -1;
			}
			else {
				return 0;
			}
		});
		for(var i = 0;i &lt; rows.length;i++) {
			tbody.appendChild(rows[i]);
		}
	}
	function makeSortable(table) {
		var headers = table.getElementsByTagName('th');
		for(var i = 0; i &lt; headers.length; i++) {
			(function(n) {
				headers[i].onclick = function() {
					sortrows(table,n)
				};
			}(i));
		}
	}
	var table =document.getElementsByTagName('table')[0];
	makeSortable(table);
[/javascript]


Demo:
<a title="简易的表格排序" href="http://code.raycn.net/demo/js/sortTable.html" target="_blank"> http://code.raycn.net/demo/js/sortTable.html</a>
