# AnjularJS + BootStrapTable 


#关键点：

    1.采用 dir-pagination-controls    
    引用 dirPagination.js
   
    2.Control 定义 加载table 的变量
       //加载table
        $scope.pageIndex=1;
        $scope.pageSize=5;
        $scope.pageCount=0;
        $scope.TotalCount=0;
        
    3.如何定义 dir-pagination-controls
     <dir-pagination-controls
        max-size="5"
        direction-links="true"
        boundary-links="true"
        on-page-change="GetData(newPageNumber)"\>
    </dir-pagination-controls>
    
     4.调用 dir-pagination-controls
       <tr dir-paginate="user in users|orderBy:sortKey:reverse|filter:search|itemsPerPage:5" total-items="TotalCount">
        <td>{{user.id}}</td>
        <td>{{user.first_name}}</td>
        <td>{{user.last_name}}</td>
        <td>{{user.hobby}}</td>
       </tr>
       
       5.实现后台调用
        $http({
                method: 'get',
                url: 'Json/mock.json',
                data: {pagesize: $scope.pageSize, pageindex: $scope.pageIndex}
            }).success(function (response) {
                $scope.users = response.data;
                $scope.TotalCount=response.total_count;
            });
        
