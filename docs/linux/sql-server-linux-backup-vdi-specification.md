---
title: VDI 備份規格 - Linux 上的 SQL Server
description: SQL Server 備份虛擬裝置介面規格。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: vanto
ms.date: 03/17/2017
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: 0250ba2b-8cdd-450e-9109-bf74f70e1247
ms.openlocfilehash: 0ee533d9a0c3dace8f7fe8ec8e0c615b444ea91d
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2020
ms.locfileid: "85892282"
---
# <a name="sql-server-on-linux-vdi-client-sdk-specification"></a>Linux 上的 SQL Server VDI 用戶端 SDK 規格

[!INCLUDE [SQL Server - Linux](../includes/applies-to-version/sql-linux.md)]

本文件涵蓋 Linux 上 SQL Server 虛擬裝置介面 (VDI) 用戶端 SDK 所提供的介面。 獨立軟體廠商 (ISV) 可以使用虛擬備份裝置應用程式開發介面 (API)，將 SQL Server 整合到產品中。 一般而言，Linux 上的 VDI 運作方式類似 Windows 上的 VDI，但有下列變更：

- Windows 共用記憶體已變成 POSIX 共用記憶體。
- Windows 旗號已變成 POSIX 旗號。
- Windows 類型 (例如 HRESULT 和 DWORD) 已變更為整數對應項。
- COM 介面已移除，並取代為一對 C++ 類別。
- Linux 上的 SQL Server 不支援具名執行個體，因此已移除執行個體名稱的參考。 
- 共用程式庫是在安裝於 /opt/mssql/lib/libsqlvdi.so 的 libsqlvdi.so 中實作

這是 **vbackup.chm** 的補充說明文件，內容詳述了 Windows 的 MS SQL Server VDI 規格。 請下載 [Windows 的 SQL VDI 規格](https://www.microsoft.com/download/details.aspx?id=17282)。

另請檢閱 [SQL Server 範例 GitHub 存放庫](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/sqlvdi-linux)中的範例 VDI 備份解決方案。

## <a name="user-permissions-setup"></a>使用者權限設定

在 Linux 上，POSIX 基本類型是由建立的使用者及其預設群組所擁有。 針對 SQL Server 所建立的物件，預設是由 mssql 使用者和 mssql 群組所擁有。 若要允許在 SQL Server 與 VDI 用戶端之間共用，有兩種建議的方法：

1. 以 mssql 使用者身分執行 VDI 用戶端
   
   執行下列命令，切換至 mssql 使用者：
   
   ```bash
   sudo su mssql
   ```

2. 將 mssql 使用者新增至 vdiuser 的群組，並將 vdiuser 新增至 mssql 群組。
   
   執行下列命令：

   ```bash
   sudo useradd vdiuser
   sudo usermod -a -G mssql vdiuser
   sudo usermod -a -G vdiuser mssql
   ```

   重新啟動伺服器，為 SQL Server 和 vdiuser 挑選新的群組

## <a name="client-functions"></a>用戶端函數

本章包含每個用戶端函數的描述。 這些描述包含下列資訊：

- 函數目的
- 函數語法
- 參數清單
- 傳回值
- 備註

## <a name="clientvirtualdevicesetcreate"></a>ClientVirtualDeviceSet::Create

**目的**：此函數會建立虛擬裝置集。

**語法**
   ```
   int ClientVirtualDeviceSet::Create (
   char *   name,       // name for the set
   VDConfig   * cfg     // configuration for the set
   );
   ```

| 參數 | 引數 | 說明
| ----- | ----- | ------ |
| | **name** | 這會識別虛擬裝置集。 必須遵循 CreateFileMapping() 所使用的名稱規則。 可使用反斜線 (\) 以外的其他字元。 這是字元字串。 建議在字串前面加上使用者的產品或公司名稱和資料庫名稱。 |
| |**cfg** | 這是虛擬裝置集的設定。 如需詳細資訊，請參閱本文件後續的＜設定＞。

| 傳回值 | 引數 | 說明
| ----- | ----- | ------ |
| |**NOERROR** | 此函數已成功。 |
| |**VD_E_NOTSUPPORTED** |設定中的一或多個欄位無效或不受支援。 |
| |**VD_E_PROTOCOL** | 虛擬裝置集已經存在。

**備註**：每個 BACKUP 或 RESTORE 作業只能呼叫一次 Create 方法。 叫用 Close 方法之後，用戶端可以重複使用此介面來建立另一個虛擬裝置集。

## <a name="clientvirtualdevicesetgetconfiguration"></a>ClientVirtualDeviceSet::GetConfiguration

**目的**：此函數是用來等候伺服器設定虛擬裝置集。
**語法**
   ```
   int ClientVirtualDeviceSet::GetConfiguration (
   time_t       timeout,    // in milliseconds
   VDConfig *       cfg // selected configuration
   );
   ```

| 參數 | 引數 | 說明
| ----- | ----- | ------ |
| | **timeout** | 這是逾時值 (以毫秒為單位)。 使用 INFINITE 或負整數，可防止逾時。
| | **cfg** | 成功執行時，這會包含伺服器所選取的設定。 如需詳細資訊，請參閱本文件後續的＜設定＞。

| 傳回值 | 引數 | 說明
| ----- | ----- | ------ |
| |**NOERROR** | 已傳回設定。
| |**VD_E_ABORT** |已叫用 SignalAbort。
| |**VD_E_TIMEOUT** |函數逾時。

**備註**：此函數會封鎖並處於「可警示」狀態。 成功叫用之後，即可開啟虛擬裝置集中的裝置。


## <a name="clientvirtualdevicesetopendevice"></a>ClientVirtualDeviceSet::OpenDevice
**目的**：此函數會開啟虛擬裝置集中的其中一部裝置。
**語法**
   ```
   int ClientVirtualDeviceSet::OpenDevice (
   char *           name,       // name for the set
   ClientVirtualDevice **       ppVirtualDevice // returns interface to device
   );
   ```

| 參數 | 引數 | 說明
| ----- | ----- | ------ |
| | **name** |這會識別虛擬裝置集。
| | **ppVirtualDevice** |當函數成功時，會傳回虛擬裝置的指標。 此裝置用於 GetCommand 和 CompleteCommand。

| 傳回值 | 引數 | 說明
| ----- | ----- | ------ |
| |**NOERROR** |此函數已成功。
| |**VD_E_ABORT** | 已要求中止。
| |**VD_E_OPEN** |  所有裝置都已開啟。
| |**VD_E_PROTOCOL** |  集合未處於初始化狀態，或此特定裝置已開啟。
| |**VD_E_INVALID** |裝置名稱無效。 這不是組成集合的其中一個已知名稱。

**備註**：可能會傳回 VD_E_OPEN 且未發生問題。 用戶端可能會透過迴圈呼叫 OpenDevice，直到傳回此代碼為止。
如果已設定多部裝置 (例如 *n* 部裝置)，虛擬裝置集會傳回 *n* 個唯一的裝置介面。

您可以使用 `GetConfiguration` 函數等到裝置可開啟為止。
如果此函數不成功，會透過 ppVirtualDevice 傳回 Null 值。
 
## <a name="clientvirtualdevicegetcommand"></a>ClientVirtualDevice::GetCommand

**目的**：此函數是用來取得下一個排入裝置佇列的命令。 要求時，此函數會等候下一個命令。

**語法**
   ```
   int ClientVirtualDevice::GetCommand (
   time_t       timeout,    // time-out in milliseconds
   VDC_Command**    ppCmd   // returns the next command
   );
   ```

| 參數 | 引數 | 說明
| ----- | ----- | ------ |
| |**timeout** |這是等候時間 (以毫秒為單位)。 使用 INFINTE 可永遠等候。 使用 0 可輪詢是否有命令。 如果目前沒有命令可用，則會傳回 VD_E_TIMEOUT。 如果發生逾時，用戶端會決定下一個動作。
| |**逾時** |這是等候時間 (以毫秒為單位)。 使用 INFINTE 或負值可永遠等候。 使用 0 可輪詢是否有命令。 如果發生逾時前沒有命令可用，會傳回 VD_E_TIMEOUT。 如果發生逾時，用戶端會決定下一個動作。
| |**ppCmd** |成功傳回命令時，參數會傳回所要執行命令的位址。 傳回的記憶體是唯讀的。 當命令完成時，此指標會傳遞至 CompleteCommand 常式。 如需每個命令的詳細資訊，請參閱本文件後續的＜命令＞。
        
| 傳回值 | 引數 | 說明
| ----- | ----- | ------ |
| |**NOERROR** |已擷取命令。
| |**VD_E_CLOSE** |伺服器已關閉裝置。
| |**VD_E_TIMEOUT** |沒有命令可用並發生逾時。
| |**VD_E_ABORT** |用戶端或伺服器已使用 SignalAbort 強制關閉。

**備註**：傳回 VD_E_CLOSE 時，SQL Server 已關閉裝置。 這是正常關機的一部分。 關閉所有裝置之後，用戶端會叫用 ClientVirtualDeviceSet::Close，關閉虛擬裝置集。
當此常式必須封鎖以等候命令時，執行緒會保留在「可警示」條件中。

## <a name="clientvirtualdevicecompletecommand"></a>ClientVirtualDevice::CompleteCommand

**目的**：此函數是用來通知 SQL Server 命令已完成。 應該會傳回適用於此命令的完成資訊。 如需詳細資訊，請參閱本文件後續的＜命令＞。

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
| |**pCmd** |這是先前從 ClientVirtualDevice::GetCommand 傳回的命令位址。
| |**completionCode** |這是指出完成狀態的狀態碼。 所有命令都必須傳回此參數。 傳回的代碼應該適用於所要執行的命令。 在所有情況下，都會使用 ERROR_SUCCESS 表示已成功執行的命令。 如需可能代碼的完整清單，請參閱 vdierror.h 檔案。 每個命令的一般狀態碼清單會出現在本文件稍後的＜命令＞。
| |**bytesTransferred** |這是已成功傳輸的位元組數。 只有資料轉送命令 Read 和 Write 會傳回此值。
| |**position** |這只是 GetPosition 命令的回應。
        
| 傳回值 | 引數 | 說明
| ----- | ----- | ------ |
| |**NOERROR** |已正確註明完成。
| |**VD_E_INVALID** |pCmd 不是使用中的命令。
| |**VD_E_ABORT** |已發出中止信號。
| |**VD_E_PROTOCOL** |裝置未開啟。

**備註**：無

## <a name="clientvirtualdevicesetsignalabort"></a>ClientVirtualDeviceSet::SignalAbort

**目的**：此函數是用來發出應該發生異常終止的信號。

**語法** 

   ```
   int ClientVirtualDeviceSet::SignalAbort ();
   ```

| 參數 | 引數 | 說明
| ----- | ----- | ------ |
| |None | 不適用
        
| 傳回值 | 引數 | 說明
| ----- | ----- | ------ |
| |**NOERROR**|已成功公佈中止通知。

**備註**：用戶端可以隨時選擇中止 BACKUP 或 RESTORE 作業。 此常式會發出所有作業都應該停止的信號。 整體虛擬裝置集的狀態會進入「異常終止」狀態。 任何裝置上都不會再傳回任何命令。 所有未完成的命令都會自動完成，並傳回 ERROR_OPERATION_ABORTED 作為完成碼。 用戶端在安全地終止提供給用戶端任何未完成使用的緩衝區之後，應該會呼叫 ClientVirtualDeviceSet::Close。 如需詳細資訊，請參閱本文件先前的＜異常終止＞。

## <a name="clientvirtualdevicesetclose"></a>ClientVirtualDeviceSet::Close

**目的**：此函數會關閉 ClientVirtualDeviceSet::Create 所建立的虛擬裝置集。 這會導致釋放所有與虛擬裝置集相關聯的資源。

**語法** 

   ```
   int ClientVirtualDeviceSet::Close ();
   ```

| 參數 | 引數 | 說明
| ----- | ----- | ------ |
| |None |不適用
        
| 傳回值 | 引數 | 說明
| ----- | ----- | ------ |
| |**NOERROR** |當虛擬裝置集已成功關閉時，就會傳回此值。
| |**VD_E_PROTOCOL** |因為虛擬裝置集未開啟，所以不會執行任何動作。
| |**VD_E_OPEN** |裝置仍處於開啟狀態。

**備註**：叫用 Close 是用戶端宣告，應該會釋放虛擬裝置集使用的所有資源。 用戶端必須確保在叫用 Close 之前，所有牽涉到資料緩衝區和虛擬裝置的活動都已終止。 Close 會使得 OpenDevice 傳回的所有虛擬裝置介面都失效。
傳回 Close 呼叫之後，用戶端才能在虛擬裝置集介面上發出 Create 呼叫。 這類呼叫會為後續的 BACKUP 或 RESTORE 作業建立新的虛擬裝置集。
如果在一或多部虛擬裝置仍處於開啟狀態時呼叫 Close，則會傳回 VD_E_OPEN。 在此情況下，會在內部觸發 SignalAbort，確保盡可能適當地關機。 這會釋放 VDI 資源。 用戶端應該等候每部裝置上的 VD_E_CLOSE 指示，再叫用 ClientVirtualDeviceSet::Close。 如果用戶端知道虛擬裝置集已處於「異常終止」狀態，則不應該預期來自 GetCommand 的 VD_E_CLOSE 指示，而且可能會在共用緩衝區上的活動終止時立即叫用 ClientVirtualDeviceSet::Close。
如需詳細資訊，請參閱本文件先前的＜異常終止＞。

## <a name="clientvirtualdevicesetopeninsecondary"></a>ClientVirtualDeviceSet::OpenInSecondary

**目的**：此函數會開啟次要用戶端中的虛擬裝置集。 主要用戶端必須已使用 Create 和 GetConfiguration 設定虛擬裝置集。

**語法** 
   
   ```
   int ClientVirtualDeviceSet::OpenInSecondary (
   char *   setName         // name of the set
   );
   ```

| 參數 | 引數 | 說明
| ----- | ----- | ------ |
| |**setName** |這會識別集合。 此名稱會區分大小寫，而且必須符合主要用戶端在叫用 ClientVirtualDeviceSet::Create 時所使用的名稱。

| 傳回值 | 引數 | 說明
| ----- | ----- | ------ |
| |**NOERROR** |此函數已成功。
| |**VD_E_PROTOCOL** |虛擬裝置集尚未建立、已在此用戶端上開啟，或虛擬裝置集尚未準備好接受來自次要用戶端的開啟要求。
| |**VD_E_ABORT** |作業即將中止。

**備註**：使用多個處理序模型時，主要用戶端會負責偵測次要用戶端的正常和異常終止。

## <a name="clientvirtualdevicesetgetbufferhandle"></a>ClientVirtualDeviceSet::GetBufferHandle

**目的**：某些應用程式可能需要多個處理序，才能在 ClientVirtualDevice::GetCommand 所傳回的緩衝區上運作。 在此情況下，接收命令的處理序可以使用 GetBufferHandle 取得處理序的獨立控制代碼來識別緩衝區。 接著可以將此控制代碼傳達給也會開啟相同虛擬裝置集的其他處理序。 該處理序接著會使用 ClientVirtualDeviceSet::MapBufferHandle，取得緩衝區的位址。 此位址可能是與其夥伴不同的位址，因為每個程序可能會對應到不同位址的緩衝區。

**語法** 

   ```
   int ClientVirtualDeviceSet::GetBufferHandle (
   uint8_t*     pBuffer,        // in: buffer address
   unsigned int*        pBufferHandle   // out: buffer handle
   );
   ```

| 參數 | 引數 | 說明
| ----- | ----- | ------ |
| |**pBuffer** |這是從 Read 或 Write 命令取得的緩衝區位址。
| |**BufferHandle** |會傳回緩衝區的唯一識別碼。

| 傳回值 | 引數 | 說明
| ----- | ----- | ------ |
| |**NOERROR** |此函數已成功。
| |**VD_E_PROTOCOL** |虛擬裝置集目前未開啟。
| |**VD_E_INVALID** |pBuffer 不是有效的位址。

備註：叫用 GetBufferHandle 函數的處理序會負責在資料轉送完成時叫用 ClientVirtualDevice::CompleteCommand。

## <a name="clientvirtualdevicesetmapbufferhandle"></a>ClientVirtualDeviceSet::MapBufferHandle

**目的**：此函數是用來從緩衝區控制代碼 (取自其他一些處理序) 取得有效的緩衝區位址。 

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
| |**ppBuffer** |這是在目前處理序中有效的緩衝區位址。

| 傳回值 | 引數 | 說明
| ----- | ----- | ------ |
| |**NOERROR** |此函數已成功。
| |**VD_E_PROTOCOL** |虛擬裝置集目前未開啟。
| |**VD_E_INVALID** |ppBuffer 是無效的控制代碼。

**備註**：請務必謹慎，以正確地傳達控制代碼。 控制代碼位於虛擬裝置集的本機。 共用控制代碼的夥伴程序，必須確保緩衝區控制代碼只在原本取得緩衝區的來源虛擬裝置集範圍內使用。


