特定作業需要連接到 SQL Server 執行個體，包括設定伺服器 (執行個體層級) 或手動將資料庫新增至可用性群組。 `sp_configure`、`RESTORE DATABASE` 等作業，或可用性群組所屬資料庫中的任何 DDL 命令，都需要連接到 SQL Server 執行個體。 根據預設，巨量資料叢集不含可連接到執行個體的端點。 您必須手動公開此端點。

如需指示，請參閱[連接到主要複本上的資料庫](../big-data-cluster/deployment-high-availability.md#instance-connect)。