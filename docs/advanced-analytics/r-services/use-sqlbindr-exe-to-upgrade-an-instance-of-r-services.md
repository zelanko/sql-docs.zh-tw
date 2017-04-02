---
title: "使用 sqlBindR.exe 升級 R Services 的執行個體 | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
applies_to: 
  - "SQL Server (starting with 2016 CTP3)"
ms.assetid: 4da80998-f929-4fad-a86f-87d09c1a79ef
caps.latest.revision: 15
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 8
---
# 使用 sqlBindR.exe 升級 R Services 的執行個體
Microsoft R Server for Windows 包含名為 **SqlBindR.exe** 的新工具，可用來升級執行個體的 R 元件。 此程序稱為**繫結**，因為它會將 SQL Server 2016 執行個體的授權模型，變成使用新的 Microsoft 新式軟體生命週期支援授權。

此授權系統通常可確保資料科學家一律使用最新版的 R。如需 Microsoft 軟體授權之條款及優點的詳細資訊，請參閱[執行 Microsoft R Server for Windows](https://msdnstage.redmond.corp.microsoft.com/en-us/microsoft-r/rserver-install-windows?branch=r-server-nov16-dev)。

當您繫結執行個體時，會發生三件事︰
+ 執行個體的支援原則會從 SQL Server 2016 支援原則變更為新的 Microsoft 新式軟體授權合約。
+ 與該執行個體相關聯的 R 元件，會在受目前新的新式軟體授權條款約束的 R Server 版本鎖定步驟中，自動隨各版本升級。
+ 執行個體不再以手動方式更新，除非是加入新套件。 

如果之後決定要停止升級各版本的執行個體，您必須**解除繫結**執行個體，然後依本文所述解除安裝 Microsoft R Server 元件︰[Run Microsoft R Server for Windows](https://msdn.microsoft.com/microsoft-r/rserver-install-windows) (執行 Microsoft R Server for Windows)。 程序完成後，未來的 R Server 升級將不再影響執行個體。

> [!NOTE] 只支援已使用累計更新 3.0 修補之 SQL Server 2016 執行個體的升級程序。  
> 
> 如果您使用的是 SQL Server vNext 的 R Services，就不需要套用這項升級。 R 元件會在每個里程碑自動升級。

## <a name="how-to-upgrade-an-instance"></a>如何升級執行個體


1. 在要升級執行個體的電腦上執行 Microsoft R server 安裝程式。
2. 請於安裝完成時，找到包含 **SqlBindR.exe** 工具的資料夾。 預設位置為：`C:\Program Files\Microsoft\R Server\Setup`
2. 以系統管理員身分開啟命令提示字元。
3. 輸入下列命令以檢視可用的執行個體清單︰`SqlBindR.exe /list`
4. 搭配 */bind* 引數執行 **SqlBindR.exe** 命令，指定要升級之執行個體的名稱。 
   例如，若只要升級預設的執行個體，請輸入︰ `SqlBindR.exe /bind MSSQL14.MSSQLSERVER`

## <a name="how-to-downgrade-an-instance-of-r-services"></a>如何降級 R Services 的執行個體

若要還原執行個體的狀態，您必須執行 SqlBindR 工具來移除授權，然後修復或重新安裝執行個體。

1. 搭配 */unbind* 引數執行 **SqlBindR.exe** 命令，並指定執行個體。 
   例如，下列命令會還原預設執行個體以符合 SQL Server 授權及 SQL Server 更新排程︰ `SqlBindR.exe /unbind MSSQL14.MSSQLSERVER`
2. 執行下列其中一項作業，將執行個體還原至其原始狀態︰
    + 修復執行個體。 修復作業會將更新套用至所有已安裝的功能。
    + 解除安裝並重新安裝，然後套用所有的服務版本。 必須重新啟動執行個體。
3. 移除 R Server 後，任何隨執行個體安裝的套件也會移除，因此必須重新安裝。

## <a name="requirements"></a>需求
僅支援符合下列需求的 SQL Server 2016 執行個體升級︰
+ SQL Server 2016 SP1 或更新版本
+ 已套用累計更新 3.0 (OD)

目前只支援使用命令列工具升級。 未來版本會提供互動式介面。

## <a name="sqlbindrexe-command-syntax"></a>sqlbindr.exe 命令語法


### <a name="usage"></a>使用方式

`sqlbindr [/list] [/bind <SQL_instance_ID>] [/unbind <SQL_instance_ID>]`

### <a name="parameters"></a>參數

|名稱|Description|
|------|------|
|*list*| 顯示目前電腦上所有 SQL 資料庫執行個體識別碼的清單|
|*bind*| 將指定的 SQL 資料庫執行個體升級到最新版 R Server，並確保執行個體自動取得 R Server 的未來升級|
|*unbind*|從指定的 SQL 資料庫執行個體解除安裝最新版的 R Server，並防止未來的 R Server 升級影響執行個體|

### <a name="errors"></a>錯誤

工具會傳回下列錯誤訊息：

|錯誤|解決方案|
|------|------|
|繫結執行個體時發生錯誤| 找不到執行個體。 請連絡支援部門以尋求協助。|
|執行個體已經繫結| 您執行了 *bind* 命令，但指定的執行個體已經繫結。 請選擇不同的執行個體。|
|執行個體尚未繫結| 您執行了 *unbind* 命令，但您指定的執行個體並未繫結。 請選擇不同的執行個體。|
|不是有效的 SQL 執行個體識別碼| 您可能輸入了錯誤的執行個體名稱。 請使用 *list* 引數再次執行命令，查看可用的執行個體識別碼。|
|找不到任何執行個體| 這部電腦沒有 SQL Server R Services 的執行個體。|
|執行個體必須安裝相容版本的 SQL R Services (資料庫內)。| 詳細資訊請參閱 https://go.microsoft.com/fwlink/?linkid=835761|
|解除繫結執行個體時發生錯誤| 無法解除繫結執行個體。 請連絡支援部門以尋求協助。|
|發生意外的錯誤| 其他錯誤。 請連絡支援部門以尋求協助。  |
|找不到任何 SQL 執行個體| 這部電腦沒有 SQL Server 的執行個體。 |


## <a name="see-also"></a>另請參閱

[R Server Release Notes](https://msdn.microsoft.com/microsoft-r/notes/r-server-notes) (R Server 版本資訊)
