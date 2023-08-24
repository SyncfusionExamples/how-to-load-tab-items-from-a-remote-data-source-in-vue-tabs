<script setup>
import { TabComponent as EjsTab, TabItemsDirective as ETabitems, TabItemDirective as ETabItem}
from "@syncfusion/ej2-vue-navigations";
import { DataManager, Query, ODataV4Adaptor } from "@syncfusion/ej2-data"; 
const onCreate = function()
{
  var obj = this.vueInstance.ej2Instances;
  
  // JSON Data Source
  // const tabData = [
  //   { header: "Steven", content: "Steven Buchanan graduated from St. Andrews University, Scotland, with a BSC degree in 1976.Upon joining the company as a sales representative in 1992, he spent 6 months in an orientation program at the Seattle office and then returned to his permanent post in London.He was promoted to sales manager in March 1993.Mr. Buchanan has completed the courses 'Successful Telemarketing' and 'International Sales Management.'He is fluent in French." },
  //   { header: "Michael", content: "Michael is a graduate of Sussex University (MA, economics, 1983) and the University of California at Los Angeles (MBA, marketing, 1986).He has also taken the courses 'Multi-Cultural Selling' and 'Time Management for the Sales Professional.'He is fluent in Japanese and can read and write French, Portuguese, and Spanish." },
  //   { header: "Robert", content: "Robert King served in the Peace Corps and traveled extensively before completing his degree in English at the University of Michigan in 1992, the year he joined the company.After completing a course entitled 'Selling in Europe,' he was transferred to the London office in March 1993." }
  // ]

  //Remote Data Source
  new DataManager({ url:'https://services.odata.org/V4/Northwind/Northwind.svc/Employees',
                   adaptor: new ODataV4Adaptor}).executeQuery(new Query().range(4,7))
                   .then((e) => {
                    var tabData = e.result;
                    var fieldMapping = { header:'FirstName', content: 'Notes'}
                    var tabItems = [];
                    for(var i=0; i<tabData.length; i++)
                    {
                    tabItems.push({ header: {text: tabData[i][fieldMapping.header] }, 
                    content: tabData[i][fieldMapping.content] });
                    obj.items = tabItems;
                    obj.refresh();
                    }
                   });
}

</script>

<template>
  <ejs-tab  cssClass="tab-content e-fill" width="850" :created="onCreate">
  </ejs-tab>
</template>

<style>
@import "../node_modules/@syncfusion/ej2-base/styles/material.css";
@import "../node_modules/@syncfusion/ej2-buttons/styles/material.css";
@import "../node_modules/@syncfusion/ej2-popups/styles/material.css";
@import "../node_modules/@syncfusion/ej2-vue-navigations/styles/material.css";

.tab-content .e-content .e-item {
    font-size: 12px;
    padding: 10px;
    text-align: justify;
}
</style>
