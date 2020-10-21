---
title: 使用 sqlcmd 連接
description: 了解如何在 Linux 和 macOS 上搭配使用 sqlcmd 公用程式與 Microsoft ODBC Driver for SQL Server。
ms.custom: ''
ms.date: 06/22/2020
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- sqlcmd
ms.assetid: 61a2ec0d-1bcb-4231-bea0-cff866c21463
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 5d69f1a19e0494b7426eebbac7d8732794f90be8
ms.sourcegitcommit: a41e1f4199785a2b8019a419a1f3dcdc15571044
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/13/2020
ms.locfileid: "91987904"
---
# <a name="connecting-with-sqlcmd"></a>使用 sqlcmd 連接
[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

[sqlcmd](../../../tools/sqlcmd-utility.md) 公用程式可在 Linux 和 macOS 上與 [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 一起使用。
  
下列命令分別說明如何使用 Windows 驗證 (Kerberos) 和 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 驗證：
  
```console
sqlcmd -E -Sxxx.xxx.xxx.xxx  
sqlcmd -Sxxx.xxx.xxx.xxx -Uxxx -Pxxx  
```  
  
## <a name="available-options"></a>可用的選項

在目前版本中，有下列選項可供使用：  
  
- -? 顯示 `sqlcmd` 使用方式。  
  
- -a 要求封包大小。  
  
- -b 如果有錯誤，則終止批次工作。  
  
- -c *batch_terminator* 指定批次結束字元。  
  
- -C 信任伺服器憑證。  

- -d *database_name* 在您啟動 `sqlcmd` 時發出 `USE` *database_name* 陳述式。  

- -D 使傳遞至 `sqlcmd` -S 選項的值解譯為資料來源名稱 (DSN)。 如需詳細資訊，請參閱本主題結尾處的＜`sqlcmd` 和 `bcp` 中的 DSN 支援＞。  
  
- -e 將輸入指令碼寫入至標準輸出裝置 (stdout)。

- -E 使用信任連接 (整合式驗證)。如需有關如何從 Linux 或 macOS 用戶端建立使用整合式驗證的信任連接的詳細資訊，請參閱[使用整合式驗證](using-integrated-authentication.md)。

- -f codepage | i:codepage[,o:codepage] | o:codepage[,i:codepage] 指定輸入和輸出字碼頁。 字碼頁碼是一個數值，指定已安裝的 Linux 字碼頁。
(自 17.5.1.1 起提供)

- -h *number_of_rows* 指定資料行標頭之間所要列印的資料列數目。  
  
- -H 指定工作站名稱。  
  
- -i *input_file*[,*input_file*[,...]] 識別包含 SQL 陳述式或預存程序之批次的檔案。  
  
- -I  將 `SET QUOTED_IDENTIFIER` 連接選項設為 [開啟]。  
  
- -k 移除或取代控制字元。  
  
- **-K**_應用程式\_意圖_  
宣告連接到伺服器時的應用程式工作負載類型。 目前唯一支援的值是 **ReadOnly**。 若未指定 **-K**，`sqlcmd` 即不支援對 AlwaysOn 可用性群組中的次要複本進行連線。 如需詳細資訊，請參閱 [Linux 和 macOS 上的 ODBC 驅動程式 - 高可用性和災害復原](odbc-driver-on-linux-support-for-high-availability-disaster-recovery.md)。  
  
> [!NOTE]  
> CTP for SUSE Linux 不支援 **-K** 。 不過，您可以在傳遞至 `sqlcmd` 的 DSN 檔案中指定 **ApplicationIntent=ReadOnly** 關鍵字。 如需詳細資訊，請參閱本主題結尾處的＜`sqlcmd` 和 `bcp` 中的 DSN 支援＞。  
  
- –l *timeout* 選項會指定在您嘗試連線到伺服器時，`sqlcmd` 登入的逾時秒數。

- -m *error_level* 控制哪些錯誤訊息會傳送至 stdout。  
  
- **-M**_多重子網路\_容錯移轉_  
在連接到 [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] 可用性群組的可用性群組接聽程式或 [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] 容錯移轉叢集執行個體時，一律指定 **-M**。 **-M** 可提供對 (目前) 作用中伺服器更快速的容錯移轉偵測與連線。 如果未指定 **-M**，則會關閉 **-M**。 如需 [!INCLUDE[ssHADR](../../../includes/sshadr_md.md)] 的詳細資訊，請參閱 [Linux 和 macOS 上的 ODBC 驅動程式 - 高可用性和災害復原](odbc-driver-on-linux-support-for-high-availability-disaster-recovery.md)。  
  
> [!NOTE]  
> CTP for SUSE Linux 不支援 **-M** 。 不過，您可以在傳遞至 `sqlcmd` 的 DSN 檔案中指定 **MultiSubnetFailover=Yes** 關鍵字。 如需詳細資訊，請參閱本主題結尾處的＜`sqlcmd` 和 `bcp` 中的 DSN 支援＞。  
  
- -N 加密連線。  
  
- -o *output_file* 識別從 `sqlcmd` 接收輸出的檔案。  
  
- -p 列印每個結果集的效能統計資料。  
  
- -P 指定使用者密碼。  
  
- -q *commandline_query* 當 `sqlcmd` 啟動時執行查詢，但查詢完成執行後不要退出。  

- -Q *commandline_query* 當 `sqlcmd` 啟動時執行查詢。 查詢完成時就會結束 `sqlcmd`。  

- -r 將錯誤訊息重新導向至 stderr。

- -R 使驅動程式使用用戶端的地區設定，將貨幣、日期和時間資料轉換成字元資料。 目前僅使用 en_US (美式英文) 格式。
  
- -s *column_separator_char* 指定資料行分隔字元。  

- -S [*protocol*:] *server*[ **,** _port_]  
指定要連接的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 執行個體；如果使用 -D，則指定 DSN。 Linux 和 macOS 上的 ODBC 驅動程式需要使用 -S。 請注意，**tcp** 是唯一有效的通訊協定。  
  
- -t *query_timeout* 指定命令 (或 SQL 陳述式) 逾時之前的秒數。  
  
- -u 指定無論 input_file 的格式為何，output_file 均以 Unicode 格式儲存。  
  
- -U *login_id* 指定使用者登入識別碼。  
  
- -V *error_severity_level* 控制用來設定 ERRORLEVEL 變數的嚴重性層級。  
  
- -w *column_width* 指定輸出的螢幕寬度。  
  
- -W 從資料行中移除尾端空格。  
  
- -x 停用變數替代。  
  
- -X 停用命令、啟動指令碼和環境變數。  
  
- -y *variable_length_type_display_width* 設定 `sqlcmd` 指令碼變數 `SQLCMDMAXFIXEDTYPEWIDTH`。
  
- -Y *fixed_length_type_display_width* 設定 `sqlcmd` 指令碼變數 `SQLCMDMAXVARTYPEWIDTH`。


## <a name="available-commands"></a>可用的命令

在目前版本中，有下列命令可供使用：  
  
-   [:]!!  
  
-   :Connect  
  
-   :Error  
  
-   [:]EXIT  
  
-   GO [*count*]  
  
-   :Help  
  
-   :List  
  
-   :Listvar  
  
-   :On Error  
  
-   :Out  
  
-   :Perftrace  
  
-   [:]QUIT  
  
-   :r  
  
-   :RESET  
  
-   :setvar  
  
## <a name="unavailable-options"></a>無法使用的選項
在目前版本中，下列選項無法使用：  

- -A 使用專用管理員連線 (DAC) 來登入 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]。 如需如何建立專用管理員連線 (DAC) 的資訊，請參閱[程式設計指導方針](programming-guidelines.md)。  
  
- -L 列出設定在本機的伺服器電腦，以及在網路中進行廣播的伺服器電腦名稱。  
  
- -v 建立 `sqlcmd` 指令碼中所能使用的 `sqlcmd` 指令碼變數。  
  
您可以使用下列替代方法：將參數放在一個檔案中，然後再附加至另一個檔案。 這將可協助您使用參數檔案來取代值。 例如，建立稱為 `a.sql` (參數檔案) 且具有下列內容的檔案：
  
```console
    :setvar ColumnName object_id  
    :setvar TableName sys.objects  
```
  
然後，建立稱為 `b.sql` 的檔案，內含要取代的參數：  
  
```sql
    select $(ColumnName) from $(TableName)  
```

在命令列上使用下列命令，將 `a.sql` 與 `b.sql` 結合為 `c.sql`：  
  
```console
    cat a.sql > c.sql 
  
    cat b.sql >> c.sql  
```
  
執行 `sqlcmd` 並使用 `c.sql` 作為輸入檔案：  
  
```console
    sqlcmd -S<...> -P<..> -U<..> -I c.sql  
```

- -z *password* 變更密碼。  
  
- -Z *password* 變更密碼並結束。  

## <a name="unavailable-commands"></a>無法使用的命令

在目前版本中，下列命令無法使用：  
  
-   :ED  
  
-   :ServerList  
  
-   :XML  
  
## <a name="dsn-support-in-sqlcmd-and-bcp"></a>sqlcmd 和 bcp 中的 DSN 支援

如果指定 `-D`，則可在 **sqlcmd** 或 **bcp** `-S` 選項 (或 **sqlcmd** :Connect 命令) 中指定資料來源名稱 (DSN)，而不是伺服器名稱。 `-D` 會使 **sqlcmd** 或 **bcp** 連線到 `-S` 選項在 DSN 中指定的伺服器。  
  
系統 DSN 會儲存在 ODBC SysConfigDir 目錄的 `odbc.ini` 檔案中 (標準安裝的 `/etc/odbc.ini`)。 使用者 DSN 會儲存在使用者主目錄的 `.odbc.ini` 中 (`~/.odbc.ini`)。

在 Windows 系統上，系統和使用者 DSN 會儲存在登錄中，並透過 odbcad32.exe 管理。 bcp 和 sqlcmd 不支援檔案 DSN。

如需驅動程式支援的項目清單，請參閱 [DSN 與連接字串關鍵字和屬性](../dsn-connection-string-attribute.md)。

DSN 中只需要 DRIVER 項目，但若要連線到遠端伺服器，則 `sqlcmd` 或 `bcp` 的 SERVER 元素中需要有值。 如果 SERVER 元素是空的或不存在於 DSN 中，則 `sqlcmd` 和 `bcp` 會嘗試連線到本機系統的預設執行個體。

在 Windows 系統上使用 bcp 時， [!INCLUDE [sssql17-md](../../../includes/sssql17-md.md)] 和較舊版本需要 SQL Native Client 11 驅動程式 (sqlncli11.dll)，而 [!INCLUDE [sssqlv15-md](../../../includes/sssqlv15-md.md)] 和更新版本則需要 Microsoft ODBC Driver 17 for SQL Server 驅動程式 (msodbcsql17.dll)。  

如果在 DSN 和 `sqlcmd` 或 `bcp` 命令列中指定相同的選項，命令列選項會覆寫 DSN 中使用的值。 例如，如果 DSN 有 DATABASE 項目，而 `sqlcmd` 命令列包含 **-d**，將會使用傳遞至 **-d** 的值。 如果在 DSN 中指定 **Trusted_Connection=yes**，則會使用 Kerberos 驗證，並且會忽略所提供的使用者名稱 ( **-U**) 和密碼 ( **-P**)。

叫用 `isql` 的現有指令碼，可藉由定義下列別名修改成使用 `sqlcmd`：`alias isql="sqlcmd -D"`。  

## <a name="see-also"></a>另請參閱  
[使用 **bcp** 進行連線](connecting-with-bcp.md)  
[版本資訊](release-notes-tools.md)
