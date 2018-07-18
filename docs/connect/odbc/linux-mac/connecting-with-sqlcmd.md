---
title: 使用 sqlcmd 連接 |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- sqlcmd
ms.assetid: 61a2ec0d-1bcb-4231-bea0-cff866c21463
caps.latest.revision: 45
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c330fd329f28fa7d89b62b9af6bb8d4bb67c2bc4
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "32853083"
---
# <a name="connecting-with-sqlcmd"></a>使用 sqlcmd 連接
[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

[Sqlcmd](http://go.microsoft.com/fwlink/?LinkID=154481)公用程式位於[!INCLUDE[msCoName](../../../includes/msconame_md.md)]ODBC Driver for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] Linux 及 macOS 上。
  
下列命令示範如何使用 Windows 驗證 (Kerberos) 和[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]驗證，分別：
  
```  
sqlcmd –E –Sxxx.xxx.xxx.xxx  
sqlcmd –Sxxx.xxx.xxx.xxx –Uxxx -Pxxx  
```  
  
## <a name="available-options"></a>可用的選項

在目前版本中，有下列選項：  
  
- -? 顯示`sqlcmd`使用量。  
  
- -要求封包大小。  
  
- -b 終止批次工作如果發生錯誤。  
  
- -c *batch_terminator*指定批次結束字元。  
  
- -C 信任伺服器憑證。  

- -d *database_name*問題`USE ` *database_name*陳述式，當您啟動`sqlcmd`。  

- -D 會使值傳遞至`sqlcmd`-S 選項可解譯為資料來源名稱 (DSN)。 如需詳細資訊，請參閱 」 中的 DSN 支援`sqlcmd`和`bcp`"本主題的結尾。  
  
- -e 會將輸入指令碼寫入標準輸出裝置 (stdout)。

- -E 使用信任的連接 （整合式驗證）。如需有關如何建立使用整合式的驗證從 Linux 或 macOS 用戶端的受信任的連線的詳細資訊，請參閱[使用整合式驗證](../../../connect/odbc/linux-mac/using-integrated-authentication.md)。

- -h *number_of_rows*指定資料行標頭之間列印的資料列數。  
  
- -H 指定工作站名稱。  
  
- -i *input_file*[，*input_file*[，...]]識別包含 SQL 陳述式的批次或預存程序的檔案。  
  
- -I 組`SET QUOTED_IDENTIFIER`連接選項設為 ON。  
  
- -k 移除或取代控制字元。  
  
- **-K * * * application_intent*  
宣告連接到伺服器時的應用程式工作負載類型。 目前唯一支援的值是 **ReadOnly**。 如果 **-K**未指定，則`sqlcmd`不支援 AlwaysOn 可用性群組中的次要複本的連接能力。 如需詳細資訊，請參閱[ODBC Driver on Linux 及 macOS-高可用性和災害復原](../../../connect/odbc/linux-mac/odbc-driver-on-linux-support-for-high-availability-disaster-recovery.md)。  
  
> [!NOTE]  
> CTP for SUSE Linux 不支援 **-K** 。 不過，您可以指定**ApplicationIntent = ReadOnly**關鍵字的 DSN 檔案中傳遞至`sqlcmd`。 如需詳細資訊，請參閱 」 中的 DSN 支援`sqlcmd`和`bcp`"本主題的結尾。  
  
- -l*逾時*指定之前的秒數`sqlcmd`登入逾時，當您嘗試連接到伺服器。

- -m *error_level*控制哪些錯誤訊息會傳送至 stdout。  
  
- **-M * * * multisubnet_failover*  
在連接到 [!INCLUDE[ssSQL11](../../../includes/sssql11_md.md)] 可用性群組的可用性群組接聽程式或 [!INCLUDE[ssSQL11](../../../includes/sssql11_md.md)] 容錯移轉叢集執行個體時，一律指定 **-M**。 **-M**提供容錯移轉，連線至 （目前） 使用中伺服器更快速的偵測。 如果未指定 **–M** ，則會關閉 **-M** 。 如需有關[!INCLUDE[ssHADR](../../../includes/sshadr_md.md)]，請參閱[ODBC Driver on Linux 及 macOS-高可用性和災害復原](../../../connect/odbc/linux-mac/odbc-driver-on-linux-support-for-high-availability-disaster-recovery.md)。  
  
> [!NOTE]  
> CTP for SUSE Linux 不支援 **-M** 。 不過，您可以指定**MultiSubnetFailover = Yes**關鍵字的 DSN 檔案中傳遞至`sqlcmd`。 如需詳細資訊，請參閱 」 中的 DSN 支援`sqlcmd`和`bcp`"本主題的結尾。  
  
- -N 加密連接。  
  
- -o *output_file*識別接收輸出的檔案`sqlcmd`。  
  
- -p 每個結果集的列印效能統計資料。  
  
- -P 指定使用者密碼。  
  
- -q *commandline_query*執行查詢時`sqlcmd`啟動，但不是會在查詢完成執行時結束。  

- -Q *commandline_query*執行查詢時`sqlcmd`啟動。 `sqlcmd` 查詢完成時，就會結束。  

- -r 重新導向錯誤訊息至 stderr。

- -R 使驅動程式將貨幣及日期和時間資料轉換成字元資料時，用於用戶端地區設定。 目前僅使用 en_US (美式英文) 格式。
  
- -s *column_separator_char*指定資料行分隔符號字元。  

- -S [*通訊協定*:]*伺服器*[**，* * * 連接埠*]  
指定的執行個體[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]連線，或如果-D 是使用，資料來源名稱。 ODBC driver on Linux 及 macOS 需要-s。 請注意， **tcp**是唯一有效的通訊協定。  
  
- -t *query_timeout*指定的命令 （或 SQL 陳述式） 逾時之前的秒數。  
  
- -u 指定該輸出檔案會儲存在 Unicode 格式，無論 input_file 的格式。  
  
- -U *login_id*指定使用者登入識別碼。  
  
- -V *error_severity_level*控制用來設定 ERRORLEVEL 變數的嚴重性層級。  
  
- -w *column_width*指定輸出的螢幕寬度。  
  
- -W 移除資料行的尾端空白。  
  
- -x 停用變數替代。  
  
- -X 停用命令、 啟動指令碼和環境變數。  
  
- -y *variable_length_type_display_width*設定`sqlcmd`指令碼變數`SQLCMDMAXFIXEDTYPEWIDTH`。
  
- -Y *fixed_length_type_display_width*設定`sqlcmd`指令碼變數`SQLCMDMAXVARTYPEWIDTH`。


## <a name="available-commands"></a>可用的命令

在目前版本中，這會提供下列的命令：  
  
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
在目前版本中，不可以使用下列選項：  

- -登入[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]利用專用的管理員連接 (DAC)。 如需如何建立專用的管理員連接 (DAC) 的資訊，請參閱[程式設計指導方針](../../../connect/odbc/linux-mac/programming-guidelines.md)。  
  
- -f*字碼頁*指定輸入和輸出字碼頁。  
  
- -L 列出設定在本機伺服器電腦，以及在網路中進行廣播的伺服器電腦名稱。  
  
- -v 建立`sqlcmd`指令碼變數可以用於`sqlcmd`指令碼。  
  
您可以使用下列替代方法： 將參數放在一個檔案，然後您可以附加到另一個檔案。 這將可協助您使用參數檔案來取代值。 例如，建立名為的檔案`a.sql`（參數檔案） 使用下列內容：
  
    :setvar ColumnName object_id  
    :setvar TableName sys.objects  
  
然後建立一個叫做檔案`b.sql`，以取代的參數：  
  
    select $(ColumnName) from $(TableName)  

在命令列中，結合`a.sql`和`b.sql`到`c.sql`使用下列命令：  
  
    cat a.sql > c.sql 
  
    cat b.sql >> c.sql  
  
執行`sqlcmd`並用`c.sql`為輸入檔：  
  
    slqcmd -S<…> -P<..> –U<..> -I c.sql  

- -z*密碼*變更密碼。  
  
- -Z*密碼*變更密碼並結束。  

## <a name="unavailable-commands"></a>無法使用的命令

在目前版本中，即無法使用下列命令：  
  
-   :ED  
  
-   :ServerList  
  
-   :XML  
  
## <a name="dsn-support-in-sqlcmd-and-bcp"></a>sqlcmd 和 bcp 中的 DSN 支援

您可以指定資料來源名稱 (DSN) 而不是中的伺服器名稱**sqlcmd**或**bcp** `-S`選項 (或**sqlcmd** : Connect 命令) 如果您指定-D. -D 會使**sqlcmd**或**bcp**連接到 DSN 中指定的-S 選項的伺服器。  
  
系統 Dsn 會儲存在`odbc.ini`ODBC SysConfigDir 目錄中的檔案 (`/etc/odbc.ini`在標準安裝)。 使用者 Dsn 會儲存在`.odbc.ini`中使用者的主目錄 (`~/.odbc.ini`)。
  
在 Linux 或 macOS DSN 中支援下列項目：

-   **ApplicationIntent = ReadOnly**  

-   **資料庫 = * * * database_name*  
  
-   **驅動程式 = ODBC Driver 11 for SQL Server**或**驅動程式 = ODBC Driver 13 for SQL Server**
  
-   **MultiSubnetFailover = Yes**  
  
-   **Server = * * * server_name_or_IP_address*  
  
-   **Trusted_Connection=yes**|**no**  
  
Dsn 中的驅動程式項目為必要項，但若要連接到伺服器，`sqlcmd`或`bcp`需要的伺服器項目中的值。  

如果在 DSN 中指定相同的選項和`sqlcmd`或`bcp`命令列命令列選項會覆寫 DSN 中使用的值。 例如，如果 DSN 有 DATABASE 項目和`sqlcmd`命令列包含 **-d**，傳遞給的值 **-d**用。 如果**Trusted_Connection = yes** DSN，會使用驗證的 Kerberos 和使用者名稱中指定 (**– U**) 和密碼 (**– P**)，如果提供，會被忽略。

叫用的現有指令碼`isql`可以修改成使用`sqlcmd`藉由定義下列別名： `alias isql="sqlcmd –D"`。  

## <a name="see-also"></a>另請參閱  
[使用連接**bcp**](../../../connect/odbc/linux-mac/connecting-with-bcp.md)  
 
