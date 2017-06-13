## <a name="pacemakerNotify"></a>了解 SQL Server 資源 pacemaker 代理程式

CTP 1.4 發行之前，可用性群組的 Pacemaker 資源代理程式可能不知道是否複本被標示為`SYNCHRONOUS_COMMIT`是否真的是最新狀態。 複本很可能已經停止與主要複本的同步處理，但未被發現。 因此代理程式無法升級的過時複本為主要-的如果成功的話，會導致資料遺失。 

加入 SQL Server 2017 CTP 1.4`sequence_number`至`sys.availability_groups`若要解決此問題。 `sequence_number`單純遞增的 BIGINT 表示如何最新的本機可用性群組複本是相對於其餘的可用性群組中的複本。 執行容錯移轉、 新增或移除複本和其他可用性群組作業會更新這個數字。 數字是在主要伺服器上，更新，然後再推送至次要複本。 因此是最新的次要複本會有相同的 sequence_number 與主要資料庫。 

當 Pacemaker 決定升級為主要複本時，會第一次傳送通知到擷取的序號，並將其儲存的所有複本 (我們稱之為預先升級通知)。 接下來，當 Pacemaker 實際上會嘗試升級為主要複本，複本只會升級本身如果其序號是從所有複本的所有序列數字的最高，否則會拒絕升級作業。 如此一來，只有序號最高的複本可以升級為主要複本，確保不會遺失資料。 

請注意，這只有在至少一個可供升級的複本與前一個主要複本具有相同序號的前提下，才能保證運作。 若要確保這種情況，預設行為是 Pacemaker 資源代理程式，以自動設定`REQUIRED_COPIES_TO_COMMIT`，至少一個同步認可次要複本是最新狀態，並可供自動容錯移轉的目標。 每個監視的動作的值與`REQUIRED_COPIES_TO_COMMIT`計算 （和更新，如有必要） 為 ('的同步認可複本 number' / 2)。 然後，在容錯移轉階段資源代理程式會要求 (`total number of replicas`  -  `required_copies_to_commit`複本) 來回應預先升級可以升級其中一個，為主要的通知。 具有最高的複本`sequence_number`會升級為主要。 

例如，讓我們考慮具有三個同步複本的一個主要複本和兩個同步認可次要複本的可用性群組的大小寫。

- `REQUIRED_COPIES_TO_COMMIT`為 3 / 2 = 1

- 所需的複本，以回應預先升級動作數目是 3-1 = 2。 因此 2 複本一定要進行容錯移轉，以觸發。 這表示，如果是主要中斷，如果其中一個次要複本沒有回應，而且只有其中一個次要資料庫會回應預先升級動作，資源代理程式無法保證回應的次要複本具有最高的 sequence_number，且不會觸發容錯移轉。

使用者可以決定是否要覆寫預設行為，以及設定可用性群組資源未設定`REQUIRED_COPIES_TO_COMMIT`自動與以上所述。

>[!IMPORTANT]
>當`REQUIRED_COPIES_TO_COMMIT`為 0 沒有資料遺失的風險。 如果是主要的中斷，資源代理程式不會自動觸發容錯移轉。 使用者必須決定是否要等候主要以復原或手動容錯移轉。

若要設定`REQUIRED_COPIES_TO_COMMIT`為 0 時，執行：

```bash
sudo pcs resource update <**ag1**> required_copies_to_commit=0
```

若要還原為預設值的計算值，執行：

```bash
sudo pcs resource update <**ag1**> required_copies_to_commit=
```

>[!NOTE]
>更新資源屬性會導致所有複本，以停止並重新啟動。 這表示主要會暫時降級為次要資料庫，然後再次升級其將 casue 暫時寫入無法使用。 REQUIRED_COPIES_TO_COMMIT 的新值才會設定之後，複本會重新啟動，因此將不會立即執行電腦命令。

## <a name="balancing-high-availability-and-data-protection"></a>平衡高可用性與資料保護 

上述的預設行為也適用於的 2 個同步複本 （主要 + 次要）。 將預設 pacemaker`REQUIRED_COPIES_TO_COMMIT = 1`以確保次要複本會自動最新狀態的最大的資料保護。  

>[!WARNING]
>這在次要複本上隨附的主要複本，因為計劃性或非計劃性中斷而無法使用較高的風險。 使用者可以選擇變更資源代理程式的預設行為，並覆寫`REQUIRED_COPIES_TO_COMMIT`設為 0:

```bash
sudo pcs resource update <**ag1**> required_copies_to_commit=0
```

一旦覆寫時，資源代理程式會使用新設定`REQUIRED_COPIES_TO_COMMIT`和停止計算。 這表示使用者必須手動加以更新據以 （例如，如果它們會增加複本的數目）。

下表描述在不同的可用性群組資源設定的主要或次要複本中斷的結果：

### <a name="availability-group---2-sync-replicas"></a>可用性群組-2 的同步處理複本

| |主要的中斷 |一個次要複本中斷
|:---|:--- |:--- |
|`REQUIRED_COPIES_TO_COMMIT=0`|使用者必須發出手動容錯移轉。 <br>可能會有資料遺失。<br> 新的主要是 R/W |主要是 R/W，以公開方式執行資料遺失
|`REQUIRED_COPIES_TO_COMMIT=1` * |叢集會自動發出容錯移轉 <br>沒有資料遺失。 <br> 先前主要資料庫會復原並聯結可用性群組做為次要資料庫之前，新的主要複本將會拒絕所有連線。 |主要將會拒絕所有連線，直到次要的復原。

\*SQL Server 資源的代理程式 Pacemaker 預設行為。

### <a name="availability-group---3-sync-replicas"></a>可用性群組-3 的同步處理複本

| |主要的中斷 |一個次要複本中斷
|:---|:--- |:--- |
|`REQUIRED_COPIES_TO_COMMIT=0`|使用者必須發出手動容錯移轉。 <br>可能會有資料遺失。 <br>新的主要是 R/W |主要是 R/W
|`REQUIRED_COPIES_TO_COMMIT=1` * |叢集會自動發出容錯移轉。 <br>沒有資料遺失。 <br>新的主要是讀寫 |主要是 R/W 

\*SQL Server 資源的代理程式 Pacemaker 預設行為。