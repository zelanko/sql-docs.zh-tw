## <a name="pacemakerNotify"></a>了解 SQL Server 的 Pacemaker 資源代理程式

在 CTP 1.4 版之前，可用性群組的 Pacemaker 資源代理程式無法得知標示為 `SYNCHRONOUS_COMMIT` 的複本是否真的為最新狀態。 複本很可能已經停止與主要複本的同步處理，但未被發現。 因此，代理程式會將過時的複本升級為主要複本 (如果成功升級則會造成資料遺失)。 

SQL Server 2017 CTP 1.4 將 `sequence_number` 新增至 `sys.availability_groups` 以解決此問題。 `sequence_number` 是依序遞增的 BIGINT，表示本機可用性群組複本相對於可用性群組其餘複本的最新更新狀態。 執行容錯移轉、新增/移除複本以及其他可用性群組作業都會更新這個數字。 這個數字會針對主要複本更新，然後推送到次要複本。 因此最新的次要複本會有與主要複本相同的 sequence_number。 

當 Pacemaker 決定要將複本升級為主要複本時，它會先傳送通知到所有複本以擷取序號並儲存它 (我們稱之為預先升級通知)。 接下來，當 Pacemaker 實際嘗試將複本升級為主要複本時，如果該複本的序號是所有複本的所有序號中最高的，就只會升級複本本身，否則會拒絕升級作業。 如此一來，只有序號最高的複本可以升級為主要複本，確保不會遺失資料。 

請注意，這只有在至少一個可供升級的複本與前一個主要複本具有相同序號的前提下，才能保證運作。 若要確保這種情況，預設行為是讓 Pacemaker 資源代理程式自動設定 `REQUIRED_COPIES_TO_COMMIT`，以便至少有一個同步認可次要複本是最新狀態，並可作為自動容錯移轉的目標。 透過每個監視動作，`REQUIRED_COPIES_TO_COMMIT` 的值會計算 (必要時並更新) 為 ('同步認可複本數' / 2)。 之後在容錯移轉時，資源代理程式會要求 (`total number of replicas` - `required_copies_to_commit` 複本) 來回應預先升級通知，以便能夠將其中一個複本升級為主要複本。 具有最高 `sequence_number` 的複本會升級為主要複本。 

例如，讓我們考慮具有三個同步複本的可用性群組案例 - 一個主要複本和兩個同步認可次要複本。

- `REQUIRED_COPIES_TO_COMMIT` 為 3 / 2 = 1

- 要回應預先升級動作的必要複本數為 3-1 = 2。 因此，必須要啟動 2 個複本，才能觸發容錯移轉。 這表示，在主要複本中斷的情況下，如果其中一個次要複本沒有回應，而且只有其中一個次要複本回應預先升級動作，資源代理程式無法保證回應的次要複本具有最高 sequence_number，因此不會觸發容錯移轉。

使用者可以選擇覆寫預設行為，並將可用性群組資源設定為不依照上述自動設定 `REQUIRED_COPIES_TO_COMMIT`。

>[!IMPORTANT]
>當 `REQUIRED_COPIES_TO_COMMIT` 為 0 時，有遺失資料的風險。 如果是主要複本中斷，資源代理程式就不會自動觸發容錯移轉。 使用者必須決定是否要等候主要複本以復原或手動容錯移轉。

若要將 `REQUIRED_COPIES_TO_COMMIT` 設定為 0 時，請執行：

```bash
sudo pcs resource update <**ag_cluster**> required_copies_to_commit=0
```

相當於使用 crm (對 SLES) 的命令為：

```bash
sudo crm resource param <**ag_cluster**> set required_synchronized_secondaries_to_commit 0
```

若要還原為預設的計算值，請執行：

```bash
sudo pcs resource update <**ag_cluster**> required_copies_to_commit=
```

>[!NOTE]
>更新資源屬性會導致所有複本停止並重新啟動。 這表示主要複本會暫時降級為次要複本，然後再次升級，因而造成暫時寫入無法使用。 REQUIRED_COPIES_TO_COMMIT 的新值只有在重新啟動複本之後才會設定，因此不會立即執行電腦命令。

## <a name="balancing-high-availability-and-data-protection"></a>平衡高可用性與資料保護 

上述的預設行為也適用於 2 個同步複本 (主要 + 次要) 的情況。 Pacemaker 將預設 `REQUIRED_COPIES_TO_COMMIT = 1`，確保次要複本會保持最新狀態，以取得最高的資料保護。  

>[!WARNING]
>由於次要複本的計劃性或非計劃性中斷，這會導致主要複本無法使用的風險較高。 使用者可以選擇變更資源代理程式的預設行為，並將 `REQUIRED_COPIES_TO_COMMIT` 覆寫為 0：

```bash
sudo pcs resource update <**ag1**> required_copies_to_commit=0
```

覆寫後，資源代理程式就會使用 `REQUIRED_COPIES_TO_COMMIT` 的新設定並停止計算。 這表示使用者必須據以手動進行更新 (比方說，如果他們增加複本的數目)。

下表描述在不同的可用性群組資源設定中主要或次要複本中斷的結果：

### <a name="availability-group---2-sync-replicas"></a>可用性群組 - 2 個同步處理複本

| |主要複本中斷 |一個次要複本中斷
|:---|:--- |:--- |
|`REQUIRED_COPIES_TO_COMMIT=0`|使用者必須發出手動 FAILOVER。 <br>可能會遺失資料。<br> 新的主要複本是 R/W |主要複本是 R/W，執行時暴露在遺失資料風險下
|`REQUIRED_COPIES_TO_COMMIT=1` * |叢集將自動發出 FAILOVER <br>無資料遺失。 <br> 在先前的主要複本復原並聯結可用性群組作為次要複本之前，新的主要複本將會拒絕所有連線。 |主要複本會拒絕所有連線，直到次要複本復原為止。

\*SQL Server 的 Pacemaker 資源代理程式預設行為。

### <a name="availability-group---3-sync-replicas"></a>可用性群組 - 3 個同步處理複本

| |主要複本中斷 |一個次要複本中斷
|:---|:--- |:--- |
|`REQUIRED_COPIES_TO_COMMIT=0`|使用者必須發出手動 FAILOVER。 <br>可能會遺失資料。 <br>新的主要複本是 R/W |主要複本是 R/W
|`REQUIRED_COPIES_TO_COMMIT=1` * |叢集將自動發出 FAILOVER。 <br>無資料遺失。 <br>新的主要複本是 RW |主要複本是 R/W 

\*SQL Server 的 Pacemaker 資源代理程式預設行為。