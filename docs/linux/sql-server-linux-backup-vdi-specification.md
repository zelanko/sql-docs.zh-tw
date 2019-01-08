---
title: VDI 備份規格-Linux 上的 SQL Server |Microsoft Docs
description: SQL Server 備份的虛擬裝置介面規格。
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 03/17/2017
ms.topic: conceptual
ms.prod: sql
ms.custom: sql-linux
ms.technology: linux
ms.assetid: 0250ba2b-8cdd-450e-9109-bf74f70e1247
ms.openlocfilehash: c43ec2c3b010d43c25b1b9f2740480952a9e9ff8
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/27/2018
ms.locfileid: "52402323"
---
# <a name="sql-server-on-linux-vdi-client-sdk-specification"></a>Linux VDI 用戶端 SDK 規格上的 SQL Server

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

本文件涵蓋 SQL Server 上 Linux 的虛擬裝置介面 (VDI) 用戶端 SDK 所提供的介面。 獨立軟體廠商 (Isv) 可以使用虛擬備份裝置的應用程式發展介面 (API)，將 SQL Server 整合到他們的產品。 一般情況下，在 Linux 上的 VDI 操作方式類似在 Windows 上的 VDI 以下列變更：

- Windows 共用的記憶體會變成 POSIX 共用記憶體。
- Windows 號誌成為 POSIX 號誌。
- Windows 型別，例如 HRESULT 和 DWORD 都會變更為整數對等項目。
- 移除和取代 c + + 類別的一組 COM 介面。
- 在 Linux 上的 SQL Server 不支援具名執行個體，因此已移除執行個體名稱的參考。 
- 在安裝於 /opt/mssql/lib/libsqlvdi.so libsqlvdi.so 中實作共用程式庫

這份文件會補充**vbackup.chm** ，詳細說明 Windows VDI 規格。 下載[Windows VDI 規格](https://www.microsoft.com/download/details.aspx?id=17282)。

同時檢閱上的 範例 VDI 備份解決方案[SQL Server 範例 GitHub 儲存機制](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/sqlvdi-linux)。

## <a name="user-permissions-setup"></a>使用者權限設定

在 Linux 上，建立以及其預設群組的使用者所擁有 POSIX 基本項目。 SQL Server 所建立的物件，這些將預設擁有 mssql 使用者和 mssql 群組。 若要讓 SQL Server 和 VDI 用戶端之間共用，下列兩種方法的其中一個建議：

1. Mssql 使用者身分執行 VDI 用戶端
   
   執行下列命令以切換至 mssql 使用者：
   
   ```bash
   sudo su mssql
   ```

2. 加入 vdiuser 的群組和 mssql 群組 vdiuser mssql 使用者。
   
   執行下列命令：

   ```bash
   sudo useradd vdiuser
   sudo usermod -a -G mssql vdiuser
   sudo usermod -a -G vdiuser mssql
   ```

   重新啟動伺服器，適用於 SQL Server 和 vdiuser 挑選新的群組

## <a name="client-functions"></a>用戶端函式

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
| | **name** | 這會識別虛擬裝置設定。 必須遵循的規則 CreateFileMapping() 所使用的名稱。 反斜線以外的任何字元 (\)可用。 這是字元字串。 建議您將前面加上使用者的產品或公司名稱和資料庫名稱的字串。 |
| |**cfg** | 這是虛擬裝置設定的組態。 如需詳細資訊，請參閱本文件稍後的 < 組態 >。

| 傳回值 | 引數 | 說明
| ----- | ----- | ------ |
| |**NOERROR** | 此函數已成功。 |
| |**VD_E_NOTSUPPORTED** |一或多個組態中的欄位無效或不支援的否則。 |
| |**VD_E_PROTOCOL** | 虛擬裝置設定已經存在。

**備註**應該只有一次呼叫建立方法，每個備份或還原作業。 叫用後關閉方法，用戶端可以重複使用介面以建立另一個虛擬裝置的集合。

## <a name="clientvirtualdevicesetgetconfiguration"></a>ClientVirtualDeviceSet::GetConfiguration

**目的**此函式用來等候要設定虛擬裝置組的伺服器。
**語法**
   ```
   int ClientVirtualDeviceSet::GetConfiguration (
   time_t       timeout,    // in milliseconds
   VDConfig *       cfg // selected configuration
   );
   ```

| 參數 | 引數 | 說明
| ----- | ----- | ------ |
| | **timeout** | 這是以毫秒為單位的逾時。 若要避免逾時，使用無限或任何負數的整數。
| | **cfg** | 成功執行後，這包含選取之伺服器的組態。 如需詳細資訊，請參閱本文件稍後的 < 組態 >。

| 傳回值 | 引數 | 說明
| ----- | ----- | ------ |
| |**NOERROR** | 傳回組態。
| |**VD_E_ABORT** |SignalAbort，叫用。
| |**VD_E_TIMEOUT** |此函式逾時。

**備註**此函式會封鎖可警示的狀態。 成功的引動過程之後, 可以開啟中的虛擬裝置設定的裝置。


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
| | **name** |這會識別虛擬裝置設定。
| | **ppVirtualDevice** |當函式成功時，則會傳回虛擬裝置的指標。 此裝置會用於 GetCommand 和 CompleteCommand 而定。

| 傳回值 | 引數 | 說明
| ----- | ----- | ------ |
| |**NOERROR** |此函數已成功。
| |**VD_E_ABORT** | 已要求中止。
| |**VD_E_OPEN** |  所有的裝置已開啟。
| |**VD_E_PROTOCOL** |  集合不是處於初始化狀態，或這個特定的裝置已開啟。
| |**VD_E_INVALID** |裝置名稱無效。 它不是其中一個已知的組成集合的名稱。

**備註**傳回 VD_E_OPEN 可能會傳回其中的問題。 用戶端可以呼叫 OpenDevice，透過迴圈，直到傳回此程式碼。
如果一個以上的裝置設定，例如*n*裝置，會傳回虛擬裝置組*n*唯一裝置介面。

`GetConfiguration`函式可用來等候，直到您可以開啟裝置。
如果此函式不成功，則會傳回透過 ppVirtualDevice null 值。
 
## <a name="clientvirtualdevicegetcommand"></a>ClientVirtualDevice::GetCommand

**目的**這個函數用來取得下一個命令排入佇列到裝置。 要求時，此函式會等候下一個命令。

**語法**
   ```
   int ClientVirtualDevice::GetCommand (
   time_t       timeout,    // time-out in milliseconds
   VDC_Command**    ppCmd   // returns the next command
   );
   ```

| 參數 | 引數 | 說明
| ----- | ----- | ------ |
| |**timeout** |這是要等待，以毫秒為單位的時間。 您可以使用無限，無限期等候。 使用 0 來輪詢命令。 如果目前使用任何命令，則會傳回 VD_E_TIMEOUT。 如果發生逾時，用戶端會決定下一個動作。
| |**逾時** |這是要等待，以毫秒為單位的時間。 若要無限期等候使用無限或負數值。 使用 0 來輪詢命令。 如果任何命令不可用，逾時到期前，會傳回 VD_E_TIMEOUT。 如果發生逾時，用戶端會決定下一個動作。
| |**ppCmd** |當命令成功傳回時，參數就會傳回要執行命令的位址。 傳回的記憶體會處於唯讀狀態。 當命令完成時，此指標會傳遞至 CompleteCommand 常式中。 如需每個命令的詳細資訊，請參閱本文件稍後的 「 命令 」。
        
| 傳回值 | 引數 | 說明
| ----- | ----- | ------ |
| |**NOERROR** |擷取命令。
| |**VD_E_CLOSE** |伺服器已關閉的裝置。
| |**VD_E_TIMEOUT** |任何命令可用而且在逾時到期。
| |**VD_E_ABORT** |用戶端或伺服器已用 SignalAbort 強制關機。

**備註**SQL Server 已關閉的裝置時，會傳回當 VD_E_CLOSE。 這是關機的正常的一部分。 所有裝置都已都關閉之後，用戶端會叫用 ClientVirtualDeviceSet::Close 來關閉虛擬裝置集。
當這個常式必須封鎖等候命令中時，執行緒會處於可警示的條件。

## <a name="clientvirtualdevicecompletecommand"></a>ClientVirtualDevice::CompleteCommand

**目的**這個函數用來通知命令完成的 SQL Server。 完成資訊適用於此命令應該會傳回。 如需詳細資訊，請參閱本文件稍後的 「 命令 」。

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
| |**pCmd** |這是先前從 ClientVirtualDevice::GetCommand 傳回命令的位址。
| |**completionCode** |這是狀態碼指出的完成狀態。 這個參數必須傳回所有命令。 傳回的程式碼應該適用於正在執行的命令。 ERROR_SUCCESS 用於所有案例中，以表示成功執行的命令。 可能的程式碼的完整清單，請參閱該檔案，vdierror.h。 每個命令的一般狀態碼清單會出現在 「 命令 」 中，在本文稍後。
| |**bytesTransferred** |這是已成功傳送的位元組數目。 這才會傳回命令的讀取和寫入的資料傳輸。
| |**position** |這是只有 GetPosition 命令的回應。
        
| 傳回值 | 引數 | 說明
| ----- | ----- | ------ |
| |**NOERROR** |完成正確註明。
| |**VD_E_INVALID** |pCmd 未作用中的命令。
| |**VD_E_ABORT** |接獲訊號中止。
| |**VD_E_PROTOCOL** |裝置未開啟。

**備註**None

## <a name="clientvirtualdevicesetsignalabort"></a>ClientVirtualDeviceSet::SignalAbort

**目的**這個函數用來表示應該發生異常終止。

**語法** 

   ```
   int ClientVirtualDeviceSet::SignalAbort ();
   ```

| 參數 | 引數 | 說明
| ----- | ----- | ------ |
| |None | 不適用
        
| 傳回值 | 引數 | 說明
| ----- | ----- | ------ |
| |**NOERROR**|中止通知成功地公佈。

**備註**在任何時間，用戶端可能會選擇中止備份或還原作業。 這個常式表示應該停止所有作業。 整體虛擬裝置組的狀態便會進入不正常終止狀態。 在任何裝置上，並未不傳回任何進一步的命令。 自動完成了所有未完成的命令，傳回 ERROR_OPERATION_ABORTED 即完成程式碼。 用戶端應該呼叫 ClientVirtualDeviceSet::Close 之後它安全地終止任何未處理的緩衝區提供給用戶端使用。 如需詳細資訊，請參閱本文件稍早的 「 異常終止 」。

## <a name="clientvirtualdevicesetclose"></a>ClientVirtualDeviceSet::Close

**目的**此函式會關閉 ClientVirtualDeviceSet::Create 所建立的虛擬裝置集合。 它會導致與虛擬裝置組相關聯的所有資源的版本。

**語法** 

   ```
   int ClientVirtualDeviceSet::Close ();
   ```

| 參數 | 引數 | 說明
| ----- | ----- | ------ |
| |None |不適用
        
| 傳回值 | 引數 | 說明
| ----- | ----- | ------ |
| |**NOERROR** |已成功關閉虛擬裝置設定時，都會傳回這個項目。
| |**VD_E_PROTOCOL** |因為虛擬裝置設定未開啟，則未不採取任何動作。
| |**VD_E_OPEN** |裝置已仍處於開啟狀態。

**備註**關閉的引動過程是用戶端宣告應該釋出虛擬裝置組所使用的所有資源。 用戶端必須確保牽涉到資料緩衝區和虛擬裝置的所有活動會都結束之前叫用 [關閉]。 OpenDevice 所傳回的所有虛擬裝置介面都被無效的關閉。
用戶端允許發出 Close 的呼叫傳回之後的虛擬裝置設定介面上的建立呼叫。 這類呼叫會建立新的虛擬裝置設定後續的備份或還原作業。
如果呼叫關閉時仍開啟一或多個虛擬裝置時，會傳回 VD_E_OPEN。 在此情況下，SignalAbort 內部觸發時，以盡可能確保正確關閉。 釋放 VDI 資源。 用戶端應該等待的 VD_E_CLOSE 指示每個裝置上叫用 ClientVirtualDeviceSet::Close 之前。 如果用戶端知道的虛擬裝置設定已處於不正常終止狀態，則它不應預期 GetCommand，VD_E_CLOSE 指示，並可能會叫用 ClientVirtualDeviceSet::Close 如共用的緩衝區上的活動會結束。
如需詳細資訊，請參閱本文件稍早的 「 異常終止 」。

## <a name="clientvirtualdevicesetopeninsecondary"></a>ClientVirtualDeviceSet::OpenInSecondary

**目的**此函式會開啟第二個用戶端中設定虛擬裝置。 主要的用戶端必須已經使用 Create 和 GetConfiguration 來設定虛擬裝置集。

**語法** 
   
   ```
   int ClientVirtualDeviceSet::OpenInSecondary (
   char *   setName         // name of the set
   );
   ```

| 參數 | 引數 | 說明
| ----- | ----- | ------ |
| |**setName** |這會識別集合。 這個名稱會區分大小寫，且必須符合 ClientVirtualDeviceSet::Create 在叫用時，主要的用戶端所使用的名稱。

| 傳回值 | 引數 | 說明
| ----- | ----- | ------ |
| |**NOERROR** |此函數已成功。
| |**VD_E_PROTOCOL** |虛擬裝置組尚未建立，此用戶端或虛擬裝置上已經開啟集還沒準備好接受來自次要的用戶端開啟要求。
| |**VD_E_ABORT** |正在中止作業。

**備註**使用多個處理序模型時，主要的用戶端負責偵測次要的用戶端的正常和異常終止。

## <a name="clientvirtualdevicesetgetbufferhandle"></a>ClientVirtualDeviceSet::GetBufferHandle

**目的**某些應用程式可能需要一個以上的程序 ClientVirtualDevice::GetCommand 所傳回的緩衝區上運作。 在這種情況下，會收到此命令的處理程序可以取得處理程序的獨立控制代碼識別緩衝區使用 GetBufferHandle。 這個控制代碼以然後告知也有相同的虛擬裝置設定已開啟任何其他處理序。 接著該程序會使用 ClientVirtualDeviceSet::MapBufferHandle 取得緩衝區的位址。 因為每個處理序對應緩衝區在不同的位址，則位址會可能比其夥伴中不同的位址。

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
| |**VD_E_PROTOCOL** |虛擬裝置組目前未開啟。
| |**VD_E_INVALID** |PBuffer 不是有效的位址。
註解 GetBufferHandle 函式會叫用的程序負責叫用 ClientVirtualDevice::CompleteCommand，資料傳輸完成時。

## <a name="clientvirtualdevicesetmapbufferhandle"></a>ClientVirtualDeviceSet::MapBufferHandle

**目的**這個函數用來取得某個其他處理序的緩衝區控制代碼從取得有效的緩衝區位址。 

**語法** 

   ```
   int ClientVirtualDeviceSet::MapBufferHandle (
   i        nt  dwBuffer,   // in: buffer handle
   uint8_t**    ppBuffer        // out: buffer address
   );
   ```

| 參數 | 引數 | 說明
| ----- | ----- | ------ |
| |**dwBuffer** |這是傳回 ClientVirtualDeviceSet::GetBufferHandle 的控制代碼。
| |**ppBuffer** |這是在目前的處理序中有效的緩衝區位址。

| 傳回值 | 引數 | 說明
| ----- | ----- | ------ |
| |**NOERROR** |此函數已成功。
| |**VD_E_PROTOCOL** |虛擬裝置組目前未開啟。
| |**VD_E_INVALID** |PpBuffer 是無效的控制代碼。

**備註**必須小心以正確地進行通訊的控制代碼。 控制代碼是單一的虛擬裝置設定的本機。 共用的控制代碼的協力電腦處理程序必須確保控制代碼只能在原先取得緩衝區已設定的虛擬裝置的範圍內使用該緩衝區。


