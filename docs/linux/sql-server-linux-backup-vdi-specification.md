---
title: "VDI 備份規格 SQL Server on Linux |Microsoft 文件"
description: "SQL Server 備份的虛擬裝置介面規格。"
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 03/17/2017
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: 
ms.suite: sql
ms.custom: sql-linux
ms.technology: database-engine
ms.assetid: 0250ba2b-8cdd-450e-9109-bf74f70e1247
ms.workload: Inactive
ms.openlocfilehash: 9760b93a1e224c35617b4161d8996ff0ed3dff67
ms.sourcegitcommit: f02598eb8665a9c2dc01991c36f27943701fdd2d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/13/2018
---
# <a name="sql-server-on-linux-vdi-client-sdk-specification"></a>Linux VDI 用戶端 SDK 規格上的 SQL Server

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

本文件包含 Linux 虛擬裝置介面 (VDI) 用戶端 SDK 上的 SQL Server 所提供的介面。 獨立軟體廠商 (Isv) 可以使用虛擬備份裝置的應用程式發展介面 (API)，若要將 SQL Server 整合到他們的產品。 一般情況下，在 Linux 上的 VDI 運作起來就像在 Windows 上的 VDI 以下列變更：

- Windows 共用的記憶體會變成 POSIX 共用記憶體。
- Windows 號誌變成 POSIX 號誌。
- Windows 型別，如 HRESULT 和 DWORD 都會變更為整數對等項目。
- 移除 COM 介面，並取代對 c + + 類別。
- SQL Server on Linux 不支援具名執行個體，因此已移除執行個體名稱的參考。 
- 安裝在 /opt/mssql/lib/libsqlvdi.so libsqlvdi.so 中實作共用程式庫

這份文件是以增補**vbackup.chm**詳述 Windows VDI 規格。 下載[Windows VDI 規格](http://www.microsoft.com/download/details.aspx?id=17282)。

也上檢閱範例 VDI 備份解決方案[SQL Server 範例 GitHub 儲存機制](http://github.com/Microsoft/sql-server-samples/tree/master/samples/features/sqlvdi-linux)。

## <a name="user-permissions-setup"></a>使用者的權限設定

在 Linux 上建立它們和其預設群組的使用者所擁有 POSIX 基本型別。 SQL Server 所建立的物件，這些將預設擁有 mssql 使用者和 mssql 群組。 若要讓 SQL Server 與 VDI 用戶端之間共用，則建議您使用下列兩種方法之一：

1. Mssql 使用者身分執行 VDI 用戶端
   
   執行下列命令，以切換到 mssql 使用者：
   
   ```bash
   sudo su mssql
   ```

2. 加入 vdiuser 群組和 mssql 群組 vdiuser mssql 使用者。
   
   執行下列命令：

   ```bash
   sudo useradd vdiuser
   sudo usermod -a -G mssql vdiuser
   sudo usermod -a -G vdiuser mssql
   ```

   重新啟動伺服器，SQL Server 和 vdiuser 挑選新的群組

## <a name="client-functions"></a>用戶端功能

此章節包含每個用戶端功能的描述。 描述包含下列資訊：

- 函式目的
- 函式語法
- 參數清單
- 傳回值
- 備註

## <a name="clientvirtualdevicesetcreate"></a>ClientVirtualDeviceSet::Create

**目的**此函式會建立虛擬裝置設定。

**語法**
   ```
   int ClientVirtualDeviceSet::Create (
   char *   name,       // name for the set
   VDConfig   * cfg     // configuration for the set
   );
   ```

| 參數 | 引數 | 說明
| ----- | ----- | ------ |
| | **name** | 這會識別虛擬裝置集合。 必須遵循 CreateFileMapping() 所使用的名稱的規則。 任何非反斜線字元 (\)可用。 這是字元字串。 建議您將前面加上使用者的產品或公司名稱和資料庫名稱的字串。 |
| |**cfg** | 這是虛擬裝置組的組態。 如需詳細資訊，請參閱本文件稍後的 < 組態 >。

| 傳回值 | 引數 | 說明
| ----- | ----- | ------ |
| |**NOERROR** | 此函數已成功。 |
| |**VD_E_NOTSUPPORTED** |一或多個組態中的欄位不正確或否則不支援。 |
| |**VD_E_PROTOCOL** | 虛擬裝置設定已經存在。

**註解**應該只有一次呼叫建立方法，每個備份或還原作業。 之後叫用之關閉方法，用戶端可以重複使用的介面來建立另一個虛擬裝置集合。

## <a name="clientvirtualdevicesetgetconfiguration"></a>ClientVirtualDeviceSet::GetConfiguration

**目的**這個函數用來等候伺服器設定的虛擬裝置設定。
**語法**
   ```
   int ClientVirtualDeviceSet::GetConfiguration (
   time_t       timeout,    // in milliseconds
   VDConfig *       cfg // selected configuration
   );
   ```

| 參數 | 引數 | 說明
| ----- | ----- | ------ |
| | **timeout** | 這是以毫秒為單位的逾時。 若要避免逾時，使用無限值或任何負數的整數。
| | **cfg** | 成功執行後，這包含選取之伺服器的組態。 如需詳細資訊，請參閱本文件稍後的 < 組態 >。

| 傳回值 | 引數 | 說明
| ----- | ----- | ------ |
| |**NOERROR** | 傳回組態。
| |**VD_E_ABORT** |SignalAbort 叫用。
| |**VD_E_TIMEOUT** |此函式已逾時。

**註解**此函式區塊中的警示狀態。 成功的引動過程之後, 會開啟虛擬裝置集合中的裝置。


## <a name="clientvirtualdevicesetopendevice"></a>ClientVirtualDeviceSet::OpenDevice
**目的**此函式會在虛擬裝置設定中開啟其中一個裝置。
**語法**
   ```
   int ClientVirtualDeviceSet::OpenDevice (
   char *           name,       // name for the set
   ClientVirtualDevice **       ppVirtualDevice // returns interface to device
   );
   ```

| 參數 | 引數 | 說明
| ----- | ----- | ------ |
| | **name** |這會識別虛擬裝置集合。
| | **ppVirtualDevice** |當函式成功時，則會傳回虛擬裝置的指標。 GetCommand 和 CompleteCommand 用於這個裝置。

| 傳回值 | 引數 | 說明
| ----- | ----- | ------ |
| |**NOERROR** |此函數已成功。
| |**VD_E_ABORT** | 已要求中止。
| |**VD_E_OPEN** |  所有的裝置皆已開啟。
| |**VD_E_PROTOCOL** |  集合不是處於初始化的狀態，或此特定裝置已開啟。
| |**VD_E_INVALID** |裝置名稱無效。 它不是其中一個已知組成集合的名稱。

**註解**VD_E_OPEN 可能會傳回沒有問題。 用戶端可以呼叫 OpenDevice，透過迴圈，直到這段程式碼會傳回。
如果多個裝置設定，例如 *n* 裝置，將會傳回虛擬裝置組 *n* 唯一裝置介面。

`GetConfiguration`函式可用來等候可以開啟裝置。
如果此函式不成功，則會傳回透過 ppVirtualDevice null 值。
 
## <a name="clientvirtualdevicegetcommand"></a>ClientVirtualDevice::GetCommand

**目的**這個函數用來取得下一個命令排入佇列到裝置。 在要求時，此函式會等候下一個命令。

**語法**
   ```
   int ClientVirtualDevice::GetCommand (
   time_t       timeout,    // time-out in milliseconds
   VDC_Command**    ppCmd   // returns the next command
   );
   ```

| 參數 | 引數 | 說明
| ----- | ----- | ------ |
| |**timeout** |這是等候，以毫秒為單位的時間。 使用 INFINTE 無限期地等待。 使用 0 輪詢命令。 如果目前使用任何命令，會傳回 VD_E_TIMEOUT。 如果發生逾時，用戶端會決定下一個動作。
| |**逾時** |這是等候，以毫秒為單位的時間。 使用 INFINTE 或負數值無限期地等待。 使用 0 輪詢命令。 如果沒有使用命令的逾時到期前，會傳回 VD_E_TIMEOUT。 如果發生逾時，用戶端會決定下一個動作。
| |**ppCmd** |當命令成功傳回時，此參數會傳回要執行的命令的位址。 傳回的記憶體為唯讀。 當命令完成時，此指標會傳遞給 CompleteCommand 常式。 如需每個命令的詳細資訊，請參閱本文件稍後的 「 命令 」。
        
| 傳回值 | 引數 | 說明
| ----- | ----- | ------ |
| |**NOERROR** |提取命令。
| |**VD_E_CLOSE** |裝置已關閉伺服器。
| |**VD_E_TIMEOUT** |任何命令可用，而且在逾時到期。
| |**VD_E_ABORT** |用戶端或伺服器已使用 SignalAbort 強制關閉。

**註解**傳回 VD_E_CLOSE 時，SQL Server 已關閉的裝置。 這是關機的正常。 在關閉所有的裝置之後，用戶端會叫用 ClientVirtualDeviceSet::Close 關閉虛擬裝置設定。
這個常式必須等候命令區塊，當執行緒處於可警示的條件。

## <a name="clientvirtualdevicecompletecommand"></a>ClientVirtualDevice::CompleteCommand

**目的**這個函數用來通知命令已完成的 SQL Server。 完成資訊適用於命令應該會傳回。 如需詳細資訊，請參閱本文件稍後的 「 命令 」。

**語法** 

   ```
   int ClientVirtualDevice::CompleteCommand (
   VDC_Command pCmd,        // the command
   int  completionCode,     // completion code
   unsigned long    bytesTransferred,   // bytes transferred
   int64_t  position        // current position
   );
   ```

| 參數 | 引數 | 說明
| ----- | ----- | ------ |
| |**pCmd** |這是所傳回 ClientVirtualDevice::GetCommand 命令的位址。
| |**completionCode** |這是狀態碼表示的完成狀態。 這個參數就必須傳回所有命令。 傳回的程式碼應該就適用於正在執行的命令。 ERROR_SUCCESS 在所有情況下用於表示已成功執行的命令。 可能的程式碼的完整清單，請參閱該檔案，vdierror.h。 每個命令的一般狀態碼清單會出現在 「 命令 」 中，在本文件稍後。
| |**bytesTransferred** |這是成功傳送的位元組數目。 這會傳回只命令讀取和寫入的資料傳輸。
| |**position** |這是只有 GetPosition 命令的回應。
        
| 傳回值 | 引數 | 說明
| ----- | ----- | ------ |
| |**NOERROR** |完成正確註明。
| |**VD_E_INVALID** |pCmd 未作用中的命令。
| |**VD_E_ABORT** |接獲訊號中止。
| |**VD_E_PROTOCOL** |裝置未開啟。

**註解**無

## <a name="clientvirtualdevicesetsignalabort"></a>ClientVirtualDeviceSet::SignalAbort

**目的**這個函數用來表示應該發生異常終止。

**語法** 

   ```
   int ClientVirtualDeviceSet::SignalAbort ();
   ```

| 參數 | 引數 | 說明
| ----- | ----- | ------ |
| |無 | 不適用
        
| 傳回值 | 引數 | 說明
| ----- | ----- | ------ |
| |**NOERROR**|中止通知已成功地公佈。

**註解**在任何時間，用戶端可能會選擇中止備份或還原作業。 這個常式發出訊號的所有作業應該都停止。 整體虛擬裝置組的狀態便會進入不正常終止狀態。 在任何裝置上，並未不傳回任何進一步的命令。 所有未完成的命令會自動完成，傳回 ERROR_OPERATION_ABORTED 完成程式碼。 用戶端應該呼叫 ClientVirtualDeviceSet::Close 後有安全地終止使用任何尚未處理完畢的緩衝區提供給用戶端。 如需詳細資訊，請參閱本文件稍早的 「 異常終止 」。

## <a name="clientvirtualdevicesetclose"></a>ClientVirtualDeviceSet::Close

**目的**此函式會關閉 ClientVirtualDeviceSet::Create 所建立的虛擬裝置設定。 它會導致與虛擬裝置組相關聯的所有資源的版本。

**語法** 

   ```
   int ClientVirtualDeviceSet::Close ();
   ```

| 參數 | 引數 | 說明
| ----- | ----- | ------ |
| |無 |不適用
        
| 傳回值 | 引數 | 說明
| ----- | ----- | ------ |
| |**NOERROR** |已成功關閉虛擬裝置設定時，都會傳回這個項目。
| |**VD_E_PROTOCOL** |未不採取任何動作，因為無法開啟虛擬裝置設定。
| |**VD_E_OPEN** |裝置尚未關閉。

**註解**關閉的引動過程是用戶端宣告應該釋出虛擬裝置集合所使用的所有資源。 用戶端必須確定資料緩衝區和虛擬裝置涉及的所有活動會叫用關閉之前都終止。 OpenDevice 所傳回的所有虛擬裝置介面都被無效的關閉。
允許用戶端發出虛擬裝置設定介面上的建立呼叫之後關閉呼叫傳回。 這類呼叫會建立新的虛擬裝置設定為後續的備份或還原操作。
如果呼叫關閉時仍開啟一或多個虛擬裝置時，會傳回 VD_E_OPEN。 在此情況下，SignalAbort 內部觸發時，以確保適當關機之下，如果可能的話。 釋放 VDI 資源。 用戶端應該等待 VD_E_CLOSE 指示每個裝置上叫用 ClientVirtualDeviceSet::Close 之前。 如果用戶端會知道虛擬裝置設定已處於不正常終止的狀態，則它不應預期 VD_E_CLOSE 指示從 GetCommand，並可能會叫用 ClientVirtualDeviceSet::Close 如終止活動上的共用緩衝區。
如需詳細資訊，請參閱本文件稍早的 「 異常終止 」。

## <a name="clientvirtualdevicesetopeninsecondary"></a>ClientVirtualDeviceSet::OpenInSecondary

**目的**此函式會開啟第二個用戶端中設定的虛擬裝置。 主要的用戶端必須具有已經使用 Create and GetConfiguration 來設定虛擬裝置集。

**語法** 
   
   ```
   int ClientVirtualDeviceSet::OpenInSecondary (
   char *   setName         // name of the set
   );
   ```

| 參數 | 引數 | 說明
| ----- | ----- | ------ |
| |**setName** |這會識別組。 這個名稱會區分大小寫，而且必須符合 ClientVirtualDeviceSet::Create 在叫用時，主要用戶端所使用的名稱。

| 傳回值 | 引數 | 說明
| ----- | ----- | ------ |
| |**NOERROR** |此函數已成功。
| |**VD_E_PROTOCOL** |虛擬裝置組尚未建立，已經開啟此用戶端或虛擬裝置上設定不是準備好接受來自次要的用戶端開啟要求。
| |**VD_E_ABORT** |正在中止作業。

**註解**使用多個處理序模型時，主要用戶端負責偵測次要的用戶端的正常和異常終止。

## <a name="clientvirtualdevicesetgetbufferhandle"></a>ClientVirtualDeviceSet::GetBufferHandle

**目的**某些應用程式可能需要在 ClientVirtualDevice::GetCommand 所傳回的緩衝區上運作的多個處理序。 在這種情況下，會在接收命令的處理程序可以用於 GetBufferHandle 取得識別緩衝區的處理程序獨立控制代碼。 這個控制代碼然後溝通也有相同的虛擬裝置設定已開啟任何其他處理序。 接著該程序會使用 ClientVirtualDeviceSet::MapBufferHandle 取得緩衝區的位址。 因為每個處理序對應於不同位址的緩衝區位址可能是比其夥伴中不同的位址。

**語法** 

   ```
   int ClientVirtualDeviceSet::GetBufferHandle (
   uint8_t*     pBuffer,        // in: buffer address
   unsigned int*        pBufferHandle   // out: buffer handle
   );
   ```

| 參數 | 引數 | 說明
| ----- | ----- | ------ |
| |**pBuffer** |這是取自讀取或寫入命令緩衝區的位址。
| |**BufferHandle** |會傳回緩衝區的唯一識別碼。

| 傳回值 | 引數 | 說明
| ----- | ----- | ------ |
| |**NOERROR** |此函數已成功。
| |**VD_E_PROTOCOL** |虛擬裝置設定不是目前開啟的。
| |**VD_E_INVALID** |PBuffer 不是有效的位址。
註解 GetBufferHandle 函式會叫用的程序會負責叫用 ClientVirtualDevice::CompleteCommand 資料傳輸完成時。

## <a name="clientvirtualdevicesetmapbufferhandle"></a>ClientVirtualDeviceSet::MapBufferHandle

**目的**這個函數用來從其他程序從取得的緩衝區控制代碼取得有效的緩衝區位址。 

**語法** 

   ```
   int ClientVirtualDeviceSet::MapBufferHandle (
   i        nt  dwBuffer,   // in: buffer handle
   uint8_t**    ppBuffer        // out: buffer address
   );
   ```

| 參數 | 引數 | 說明
| ----- | ----- | ------ |
| |**dwBuffer** |這是 ClientVirtualDeviceSet::GetBufferHandle 所傳回的控制代碼。
| |**ppBuffer** |這是在目前的處理序中有效的緩衝區位址。

| 傳回值 | 引數 | 說明
| ----- | ----- | ------ |
| |**NOERROR** |此函數已成功。
| |**VD_E_PROTOCOL** |虛擬裝置設定不是目前開啟的。
| |**VD_E_INVALID** |PpBuffer 是無效的控制代碼。

**註解**必須特別小心正確通訊控點。 控制代碼是單一的虛擬裝置設定的本機。 共用的控制代碼的夥伴處理程序必須確保該控制代碼可用只能在原先取得緩衝區已設定的虛擬裝置的範圍內的緩衝區。


