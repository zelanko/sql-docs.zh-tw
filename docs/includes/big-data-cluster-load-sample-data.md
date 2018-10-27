### <a id="sampledata"></a> 載入範例資料

SQL Server 巨量資料叢集教學課程都使用一組常用的範例資料。 若要設定範例資料在您的巨量資料叢集上使用下列步驟：

1. 如果您沒有 SQL Server 命令列工具 (**sqlcmd**並**bcp**) 安裝，請先安裝這些工具與其中一個連結：

   * **Windows**:[安裝 SQL Server 在 Windows 上的命令列工具](https://www.microsoft.com/download/details.aspx?id=53591)
   * **Linux**: [Linux 上的 SQL Server 安裝命令列工具](https://docs.microsoft.com/sql/linux/sql-server-linux-setup-tools)

1. 下載範例的備份檔案[tpcxbb_1gb.bak](https://sqlchoice.blob.core.windows.net/sqlchoice/static/tpcxbb_1gb.bak)到您的電腦。

1. 瀏覽至 SQL Server 2019 巨量資料叢集[範例目錄](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/sql-big-data-cluster)。

1. 下載[啟動程序-範例-db.sql](https://github.com/Microsoft/sql-server-samples/blob/master/samples/features/sql-big-data-cluster/bootstrap-sample-db.sql) Transact SQL 指令碼。

1. 下載並從命令列執行下列兩個範例指令碼的其中一個：

   * **Windows**:[啟動程序-範例-db.cmd](https://github.com/Microsoft/sql-server-samples/blob/master/samples/features/sql-big-data-cluster/bootstrap-sample-db.cmd)
   * **Linux**:[啟動程序-範例-db.sh](https://github.com/Microsoft/sql-server-samples/blob/master/samples/features/sql-big-data-cluster/bootstrap-sample-db.sh)

   > [!TIP]
   > 您可以不含任何參數執行指令碼，以取得使用方式指示。

指令碼會將範例資料庫還原至 SQL Server 的主要執行個體，並也會將資料載入 HDFS 儲存體集區中。