---
title: 以指令碼變數使用 sqlcmd | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.technology: scripting
ms.reviewer: ''
ms.topic: conceptual
dev_langs:
- TSQL
helpviewer_keywords:
- scripts [SQL Server], sqlcmd utility
- variables [SQL Server], scripts
- scripting variables [SQL Server]
- sqlcmd utility, scripts
- setvar command
ms.assetid: 793495ca-cfc9-498d-8276-c44a5d09a92c
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 5ec665895be835848ab3b1ed8b8d90583aa31576
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47643426"
---
# <a name="sqlcmd---use-with-scripting-variables"></a>sqlcmd - 搭配指令碼變數使用
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
  用於指令碼中的變數稱為指令碼變數。 指令碼變數可讓一個指令碼使用於多個狀況中。 例如，如果您想要針對多個伺服器執行一個指令碼，而不針對每個伺服器修改指令碼，您可以使用指令碼變數來代表伺服器名稱。 只要變更提供給指令碼變數的伺服器名稱，相同的指令碼就可以在不同的伺服器上執行。  
  
 指令碼變數可以使用 **setvar** 命令來明確定義，或使用 **sqlcmd-v** 選項來隱含定義。  
  
 本主題也包含在 Cmd.exe 命令提示字元中使用 **SET**來定義環境變數的範例。  
  
## <a name="setting-scripting-variables-by-using-the-setvar-command"></a>使用 setvar 命令設定指令碼變數  
 **setvar** 命令可用來定義指令碼變數。 使用 **setvar** 命令定義的變數會儲存在內部。 指令碼變數不應與在命令提示字元中使用 **SET**所定義的環境變數產生混淆。 如果指令碼參考非環境變數的變數，或不是使用 **setvar**所定義的變數，則會傳回錯誤訊息並停止執行指令碼。 如需詳細資訊，請參閱 **sqlcmd 公用程式** 中的 [-b](../../tools/sqlcmd-utility.md)選項。  
  
## <a name="variable-precedence-low-to-high"></a>變數優先順序 (由低至高)  
 如果有多個類型的變數具有相同的名稱，會使用具有最高優先順序的變數。  
  
1.  系統層級環境變數  
  
2.  使用者層級環境變數  
  
3.  在啟動**SET X=Y**之前，於命令提示字元設定命令殼層 ( **SET X=Y**)  
  
4.  **sqlcmd-v** X=Y  
  
5.  **:Setvar** X Y  
  
> [!NOTE]  
>  若要檢視環境變數，請在 [控制台] 中開啟 [系統] ，然後按一下 [進階]  索引標籤。  
  
## <a name="implicitly-setting-scripting-variables"></a>隱含設定指令碼變數  
 當您透過含有 **sqlcmd** 相關變數的選項啟動 **sqlcmd** 時，會將 **sqlcmd** 變數隱含設定為使用該選項所指定的值。 在下列範例中， `sqlcmd` 透過 `-l` 選項啟動。 這將會隱含地設定 SQLLOGINTIMEOUT 變數。  
  
```
c:\> sqlcmd -l 60
```
 
您也可以使用 **-v** 選項來設定存在於指令碼中的指令碼變數。 在下列指令碼 (檔名為 `testscript.sql`) 中， `ColumnName` 為指令碼變數。  
 
```
USE AdventureWorks2012;

SELECT x.$(ColumnName)
FROM Person.Person x
WHERE x.BusinessEntityID < 5;
```

您可以接著指定要使用 `-v` 選項傳回的資料行名稱：  
 
```
sqlcmd -v ColumnName ="FirstName" -i c:\testscript.sql
```

若要使用相同的指令碼傳回不同的資料行，請變更 `ColumnName` 指令碼變數的值。  
  
```
sqlcmd -v ColumnName ="LastName" -i c:\testscript.sql
```

## <a name="guidelines-for-scripting-variable-names-and-values"></a>指令碼變數名稱和值的指導方針  
 當您為指令碼變數命名時，請考慮下列指導方針：  
  
-   變數名稱不能包含空白字元或引號。  
  
-   變數名稱的格式不能和變數運算式的格式相同，例如 *$(var)*。  
  
-   指令碼變數不區分大小寫。  
  
    > [!NOTE]  
    >  如果未指定任何值給 **sqlcmd** 環境變數，則會移除該變數。 使用未含值的 **:setvar VarName** ，會清除變數。  
  
 當您指定指令碼變數的值時，請考慮下列指導方針：  
  
-   如果字串值包含空格，則使用 **setvar** 或 **-v** 選項所定義的變數值必須用引號括住。  
  
-   如果引號是變數值的一部分，則必須逸出。 例如：`setvar MyVar "spac""e"`。  
  
## <a name="guidelines-for-cmdexe-set-variable-values-and-names"></a>Cmd.exe SET 變數值和名稱的指導方針  
 使用 SET 所定義的變數是 Cmd.exe 環境的一部分，並且可供 **sqlcmd**參考。 請考慮下列指導方針：  
  
-   變數名稱不能包含空白字元或引號。  
  
-   變數值可以包含空格或引號。  
  
## <a name="sqlcmd-scripting-variables"></a>sqlcmd 指令碼變數  
 由 **sqlcmd** 定義的變數稱為指令碼變數。 下表列出 **sqlcmd** 指令碼變數。  
  
|        變數         | 相關的選項 | R/W |         預設         |
| ----------------------- | -------------- | --- | ----------------------- |
| SQLCMDUSER\*             | -U             | R   | ""                      |
| SQLCMDPASSWORD\*         | -P             | --  | ""                      |
| SQLCMDSERVER\*           | -S             | R   | "DefaultLocalInstance"  |
| SQLCMDWORKSTATION       | -H             | R   | "ComputerName"          |
| SQLCMDDBNAME            | -d             | R   | ""                      |
| SQLCMDLOGINTIMEOUT      | -l             | R/W | "8" (秒)           |
| SQLCMDSTATTIMEOUT       | -t             | R/W | "0" = 永遠等候 |
| SQLCMDHEADERS           | -H             | R/W | "0"                     |
| SQLCMDCOLSEP            | -S             | R/W | 「 」                     |
| SQLCMDCOLWIDTH          | -w             | R/W | "0"                     |
| SQLCMDPACKETSIZE        | -A             | R   | "4096"                  |
| SQLCMDERRORLEVEL        | -M             | R/W | "0"                     |
| SQLCMDMAXVARTYPEWIDTH   | -y             | R/W | "256"                   |
| SQLCMDMAXFIXEDTYPEWIDTH | -y             | R/W | "0" = 無限制         |
| SQLCMDEDITOR            |                | R/W | "edit.com"              |
| SQLCMDINI               |                | R   | ""                      |

* SQLCMDUSER、SQLCMDPASSWORD 和 SQLCMDSERVER 會在使用 **:Connect** 時設定。  

R 表示在程式初始化期間只能設定該值一次。  
  
R/W 表示可以使用 **setvar** 命令來重設該值，且後續的命令將會使用新值。  
  
## <a name="examples"></a>範例  
  
### <a name="a-using-the-setvar-command-in-a-script"></a>A. 在指令碼中使用 setvar 命令  
 許多 **sqlcmd** 選項可以在指令碼中使用 **setvar** 命令來控制。 下列範例會建立指令碼 `test.sql` ，其中的 `SQLCMDLOGINTIMEOUT` 變數設為 `60` 秒，而另一個指令碼變數 `server`則設為 `testserver`。 下列程式碼是在 `test.sql`中。  

```
:setvar SQLCMDLOGINTIMEOUT 60
:setvar server "testserver"
:connect $(server) -l $(SQLCMDLOGINTIMEOUT)

USE AdventureWorks2012;

SELECT FirstName, LastName
FROM Person.Person;
```

隨後會使用 sqlcmd 呼叫指令碼：

```
sqlcmd -i c:\test.sql
```
  
### <a name="b-using-the-setvar-command-interactively"></a>B. 以互動方式使用 setvar 命令  
 下列範例顯示如何使用 `setvar` 命令，以互動方式設定指令碼變數。  

```
sqlcmd
:setvar  MYDATABASE AdventureWorks2012
USE $(MYDATABASE);
GO
```

 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```
Changed database context to 'AdventureWorks2012'
1>
```
  
### <a name="c-using-command-prompt-environment-variables-within-sqlcmd"></a>C. 在 sqlcmd 內使用命令提示字元環境變數  
 在下列範例中，設定了四個環境變數 `are` ，然後從 `sqlcmd`進行呼叫。  

```
C:\>SET tablename=Person.Person
C:\>SET col1=FirstName
C:\>SET col2=LastName
C:\>SET title=Ms.
C:\>sqlcmd -d AdventureWorks2012
1> SELECT TOP 5 $(col1) + ' ' + $(col2) AS Name
2> FROM $(tablename)
3> WHERE Title ='$(title)'
4> GO
```
  
### <a name="d-using-user-level-environment-variables-within-sqlcmd"></a>D. 在 sqlcmd 內使用使用者層級環境變數  
 下列範例在命令提示字元中設定了使用者層級環境變數 `%Temp%`，並將其傳遞至 `sqlcmd` 輸入檔。 若要取得使用者層級環境變數，請在 [控制台] 中按兩下 [系統]。 按一下 [進階] 索引標籤，然後按一下 [環境變數]。  
  
 下列程式碼是在輸入檔 `c:\testscript.txt` 中：

```
:OUT $(MyTempDirectory)
USE AdventureWorks2012;

SELECT FirstName
FROM AdventureWorks2012.Person.Person
WHERE BusinessEntityID` `< 5;
```

下列程式碼是在命令提示字元中輸入的：

```
C:\ >SET MyTempDirectory=%Temp%\output.txt
C:\ >sqlcmd -i C:\testscript.txt
```

 下列結果會傳送到輸出檔 C:\Documents and Settings\\<使用者\>\Local Settings\Temp\output.txt。  

```
Changed database context to 'AdventureWorks2012'.
FirstName
--------------------------------------------------
Gustavo
Catherine
Kim
Humberto

(4 rows affected)
```

### <a name="e-using-a-startup-script"></a>E. 使用啟動指令碼  
 啟動 **sqlcmd** 時，會執行 **sqlcmd** 啟動指令碼。 下列範例會設定環境變數 `SQLCMDINI`。 這是下者的內容： `init.sql.`  

```
SET NOCOUNT ON
GO

DECLARE @nt_username nvarchar(128)
SET @nt_username = (SELECT rtrim(convert(nvarchar(128), nt_username))
FROM sys.dm_exec_sessions WHERE spid = @@SPID)
SELECT  @nt_username + ' is connected to ' +
rtrim(CONVERT(nvarchar(20), SERVERPROPERTY('servername'))) +
' (' +`  
rtrim(CONVERT(nvarchar(20), SERVERPROPERTY('productversion'))) +
')'
:setvar SQLCMDMAXFIXEDTYPEWIDTH 100
SET NOCOUNT OFF
GO

:setvar SQLCMDMAXFIXEDTYPEWIDTH
```

 這會在 `init.sql` 啟動時呼叫 `sqlcmd` 檔案。  
  
```
c:\> SET sqlcmdini=c:\init.sql
>1 Sqlcmd
```

 以下是輸出。  

```
>1 < user > is connected to < server > (9.00.2047.00)
```

  
> [!NOTE]  
>  **-X** 選項會停用啟動指令碼功能。  
  
### <a name="f-variable-expansion"></a>F. 變數展開  
 下列範例顯示如何以 **sqlcmd** 變數的形式來使用資料。  

```
USE AdventureWorks2012;
CREATE TABLE AdventureWorks2012.dbo.VariableTest
(
Col1 nvarchar(50)
);
GO
```

 在 `Col1` 的 `dbo.VariableTest` 中插入一個資料列，內含值 `$(tablename)`。  

```
INSERT INTO AdventureWorks2012.dbo.VariableTest(Col1)
VALUES('$(tablename)');
GO
```
  
 在 `sqlcmd` 提示字元中，當沒有任何變數設定為等於 `$(tablename)`時，下列陳述式會傳回資料列。  
  
```
C:\> sqlcmd
>1 SELECT Col1 FROM dbo.VariableTest WHERE Col1 = '$(tablename)';
>2 GO
>3 SELECT Col1 FROM dbo.VariableTest WHERE Col1 = N'$(tablename)';
>4 GO
```

[!INCLUDE[ssResult](../../includes/ssresult-md.md)]  

```
>1 Col1
>2 ------------------
>3 $(tablename)
>4
>5 (1 rows affected)
```

 假使變數 `MyVar` 設定為 `$(tablename)`。  

```
>6 :setvar MyVar $(tablename)
```

 下列陳述式會傳回該資料列，而且還會傳回訊息「'tablename' 指令碼變數未定義」。  

```
>6 SELECT Col1 FROM dbo.VariableTest WHERE Col1 = '$(tablename)';
>7 GO

>1 SELECT Col1 FROM dbo.VariableTest WHERE Col1 = N'$(tablename)';
>2 GO
```

 下列陳述式會傳回資料列。  

```
>1 SELECT Col1 FROM dbo.VariableTest WHERE Col1 = '$(MyVar)';
>2 GO
```

```
>1 SELECT Col1 FROM dbo.VariableTest WHERE Col1 = N'$(MyVar)';
>2 GO
```
  
## <a name="see-also"></a>另請參閱  
 [使用 sqlcmd 公用程式](../../relational-databases/scripting/sqlcmd-use-the-utility.md)   
 [-b](../../tools/sqlcmd-utility.md)   
 [命令提示字元公用程式參考 &#40;Database Engine&#41;](../../tools/command-prompt-utility-reference-database-engine.md)  
  
  
