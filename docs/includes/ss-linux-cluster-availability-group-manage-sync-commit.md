## <a name="managing-synchronous-commit-mode"></a>管理同步認可模式

>[!WARNING]
>在某些情況下，Linux 上處於同步認可模式的 SQL Server 可用性群組可能容易發生資料遺失。 請查看下列詳細資料以了解根本原因，以及可確保避免資料遺失的因應措施。 此問題將會在即將發行的版本中修正。

###<a name="pacemaker-notification-for-availability-group-resource-promotion"></a>可用性群組資源升級的 Pacemaker 通知

在 CTP 1.4 版之前，可用性群組的 Pacemaker 資源代理程式無法得知標示為 `SYNCHRONOUS_COMMIT` 的複本是否真的為最新狀態。 複本很可能已經停止與主要複本的同步處理，但未被發現。 因此，代理程式會將過時的複本升級為主要複本 (如果成功升級則會造成資料遺失)。 

SQL Server vNext CTP 1.4 將 `sequence_number` 加入到 `sys.availability_groups` 以解決此問題。 `sequence_number` 是依序遞增的 BIGINT，表示本機 AG 複本相對於系統其餘部分的最新更新狀態。 執行容錯移轉、新增/移除複本以及其他 AG 作業都會更新這個數字。 這個數字會針對主要複本更新，然後推送到次要複本。 因此最新的次要複本會有與主要複本相同的數字。

當 Pacemaker 決定要將複本升級為主要複本時，它會先傳送通知到所有複本以擷取序號並儲存它。 接下來，當 Pacemaker 實際嘗試將複本升級為主要複本時，如果該複本的序號是所有序號中最高的，則只會升級複本本身，否則會拒絕升級作業。 如此一來，只有序號最高的複本可以升級為主要複本，確保不會遺失資料。

請注意，這只有在至少一個可供升級的複本與前一個主要複本具有相同序號的前提下，才能保證運作。 因為資源代理程式需要 Pacemaker 傳送通知到所有複本，可用性資源必須以 `notify=true` 設定。 針對每個現有的 `ocf:mssql:ag` 資源，使用者將需要以 `notify=true` 更新資源組態，然後才能將 `mssql-server-ha` 套件更新至 CTP 1.4，否則資源將會進入錯誤狀態。 

### <a name="how-to-avoid-potential-for-data-loss"></a>如何避免資料遺失的可能性 

在下列情況中，可用性群組仍可能遺失資料。 在包含五個節點的叢集中，如果在三個 SQL Server 執行個體上存在含有複本的可用性群組，則主要複本及一個次要複本可能位在其他次要複本之前。 當它們在前面時，`sys.availability_groups` 中的 `sequence_number` 會高於其他複本。 在這種情況下，如果這兩個複本失去與叢集其餘節點的連線，Pacemaker 可能會將剩餘的三個節點視為仲裁，並允許潛在複本將自己提升為主要複本。 此情況下就可能會遺失資料。

sqlVnext 導入了新功能，可強制特定數目的次要複本必須是可用的，才能認可主要複本上的任何交易。 `REQUIRED_COPIES_TO_COMMIT` 可讓您設定繼續交易之前，必須認可到次要複本資料庫交易記錄的複本數目。 您可以使用此選項搭配 `CREATE AVAILABILITY GROUP` 或 `ALTER AVAILABILITY GROUP`。 請參閱 [CREATE AVAILABILITY GROUP](http://msdn.microsoft.com/library/ff878399.aspx)。

若要避免上述資料遺失的可能性，請將 `REQUIRED_COPIES_TO_COMMIT` 設定為已同步處理複本的最大數目。 即將發行的版本將會內建自動處理設定 `REQUIRED_COPIES_TO_COMMIT` 的邏輯。
當設定 `REQUIRED_COPIES_TO_COMMIT` 後，主要複本資料庫的交易會等候，直到交易在要求的同步次要複本資料庫交易記錄數目上認可為止。 如果在線上的同步次要複本不足，則交易會停止，直到與足夠次要複本的通訊繼續為止。

下列範例會將可用性群組名稱 [ag1] 設定為 `REQUIRED_COPIES_TO_COMMIT = 2`。 

```Transact-SQL
ALTER AVAILABILITY GROUP [ag1]
SET (REQUIRED_COPIES_TO_COMMIT = 2)
```

在上述範例中，如果可用性群組有兩個次要複本，它會等到兩個次要複本都確認認可為止。 如果其中一個變成無法回應，則會封鎖交易。
