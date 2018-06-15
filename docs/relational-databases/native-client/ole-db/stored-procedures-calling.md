---
title: 呼叫預存程序 (OLE DB) |Microsoft 文件
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: native-client-ole-db
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- calling stored procedures
- RPC escape sequence
- OLE DB, stored procedures
- parameters [SQL Server Native Client], OLE DB
- ODBC CALL escape sequence
- stored procedures [OLE DB], calling
- SQL Server Native Client OLE DB provider, stored procedures
ms.assetid: 8e5738e5-4bbe-4f34-bd69-0c0633290bdd
caps.latest.revision: 39
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: e853d37f3ada75ef5259fbc8fedabfb3e48d8c9d
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "32954913"
---
# <a name="stored-procedures---calling"></a>預存程序的呼叫
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  預存程序可以有零或多個參數。 它也可以傳回值。 當使用[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native Client OLE DB 提供者，可以傳遞預存程序的參數：  
  
-   將資料值寫入程式碼。  
  
-   使用參數標記 (?) 來指定參數、將程式變數繫結至參數標記，然後將資料值放在程式變數中。  
  
> [!NOTE]  
>  搭配 OLE DB 使用具名參數呼叫 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 預存程序時，參數名稱開頭必須是 '@' 字元。 這是一個 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 特定的限制。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者會比 MDAC 更嚴格地強制執行此限制。  
  
 若要支援的參數， **ICommandWithParameters** command 物件上公開介面。 若要使用參數，取用者會先描述提供者的參數呼叫**icommandwithparameters:: Setparameterinfo**方法 (或選擇性地準備呼叫的呼叫陳述式**GetParameterInfo**方法)。 接著，取用者會建立指定緩衝區結構的存取子，並將參數值放在此緩衝區中。 最後，它會存取子和一個指標的控制代碼傳遞至緩衝區**Execute**。 稍後呼叫**Execute**，取用者會將新的參數值放在緩衝區中，並呼叫**Execute**存取子控制代碼和緩衝區指標。  
  
 呼叫暫存預存程序使用參數的命令必須先呼叫**icommandwithparameters:: Setparameterinfo**定義的參數資訊，可以成功準備命令之前。 這是因為暫存預存程序的內部名稱與用戶端所使用的外部名稱不同，而且 SQLOLEDB 無法查詢系統資料表來判斷暫存預存程序的參數資訊。  
  
 以下是參數繫結程序中的步驟：  
  
1.  在 DBPARAMBINDINFO 結構的陣列中填入參數資訊；也就是參數名稱、參數資料類型的提供者專屬名稱，或標準資料類型名稱等等。 陣列中的每個結構會描述一個參數。 這個陣列會傳遞至**SetParameterInfo**方法。  
  
2.  呼叫**icommandwithparameters:: Setparameterinfo**方法來描述提供者的參數。 **SetParameterInfo**指定每個參數的原生資料類型。 **SetParameterInfo**引數是：  
  
    -   用於設定類型資訊之參數的數目。  
  
    -   用於設定類型資訊之參數序數的陣列。  
  
    -   DBPARAMBINDINFO 結構的陣列。  
  
3.  建立參數存取子使用**iaccessor:: Createaccessor**命令。 存取子會指定緩衝區的結構，並將參數值放在緩衝區中。 **CreateAccessor**命令會從一組繫結建立存取子。 這些繫結可由取用者使用 DBBINDING 結構的陣列描述。 每個繫結都會與取用者緩衝區的單一參數產生關聯，而且會包含資訊，例如：  
  
    -   套用繫結之參數的序數。  
  
    -   繫結的項目 (資料值、其長度及其狀態)。  
  
    -   緩衝區中對每一個部分的位移。  
  
    -   存在於取用者緩衝區內之資料值的長度和類型。  
  
     存取子是由其類型為 HACCESSOR 的控制代碼識別。 這個控制代碼由**CreateAccessor**方法。 每當取用者完成使用存取子時，取用者必須呼叫**ReleaseAccessor**方法，以釋放所保留的記憶體。  
  
     當取用者呼叫方法，例如**icommand:: Execute**，將控制代碼傳遞至存取子以及緩衝區本身的指標。 提供者會使用此存取子決定如何傳送包含在緩衝區中的資料。  
  
4.  填入 DBPARAMS 結構。 在執行階段所傳遞值取自從哪一個輸入參數和值寫入至輸出參數的取用者變數**icommand:: Execute** DBPARAMS 結構。 DBPARAMS 結構包含三個元素：  
  
    -   根據存取子控制代碼指定的繫結，提供者從其中擷取輸入參數資料的緩衝區指標以及提供者傳回輸出參數資料的緩衝區指標。  
  
    -   緩衝區中的參數集數目。  
  
    -   存取子控制代碼會在步驟 3 中建立。  
  
5.  執行此命令使用**icommand:: Execute**。  
  
## <a name="methods-of-calling-a-stored-procedure"></a>呼叫預存程序的方法  
 執行中的預存程序時[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者支援:  
  
-   ODBC CALL 逸出序列。  
  
-   遠端程序呼叫 (RPC) 逸出序列。  
  
-   [!INCLUDE[tsql](../../../includes/tsql-md.md)] EXECUTE 陳述式。  
  
### <a name="odbc-call-escape-sequence"></a>ODBC CALL 逸出序列  
 如果您知道參數資訊，請呼叫**icommandwithparameters:: Setparameterinfo**方法來描述提供者的參數。 否則，在呼叫預存程序中使用 ODBC CALL 語法時，提供者會呼叫 Helper 函數來尋找預存程序參數資訊。  
  
 如果您不確定參數資訊 (參數中繼資料)，建議使用 ODBC CALL 語法。  
  
 使用 ODBC CALL 逸出序列呼叫程序的一般語法為：  
  
 {[**?=**]**call***procedure_name*[**(**[*parameter*][**,**[*parameter*]]...**)**]}  
  
 例如：  
  
```  
{call SalesByCategory('Produce', '1995')}  
```  
  
### <a name="rpc-escape-sequence"></a>RPC 逸出序列  
 RPC 逸出序列類似於呼叫預存程序的 ODBC CALL 語法。 如果您要呼叫程序數次，RPC 逸出序列會在呼叫預存程序的三種方法之間，提供最佳效能。  
  
 當 RPC 逸出序列用於執行預存程序時，提供者不會呼叫任何 Helper 函數來判斷參數資訊 (如果是 ODBC CALL 語法，則會這麼做)。 RPC 語法比 ODBC CALL 語法簡單，因此命令集的剖析速度較快，可以增進效能。 在此情況下，您需要提供參數資訊，藉由執行**icommandwithparameters:: Setparameterinfo**。  
  
 RPC 逸出序列要求您擁有傳回值。 如果預存程序沒有傳回值，伺服器預設會傳回 0。 此外，您無法在預存程序上開啟 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 資料指標。 預存程序會以隱含方式準備和呼叫**icommandprepare:: Prepare**將會失敗。 由於無法準備 RPC 呼叫，您可以查詢資料行中繼資料;Icolumnsinfo:: Getcolumninfo 和 icolumnsrowset:: Getcolumnsrowset 將會傳回 DB_E_NOTPREPARED。  
  
 如果您知道所有參數中繼資料，RPC 逸出序列是執行預存程序的建議方式。  
  
 這是呼叫預存程序之 RPC 逸出序列的範例：  
  
```  
{rpc SalesByCategory}  
```  
  
 示範 RPC 逸出序列的範例應用程式，請參閱[執行預存程序 & #40;使用 RPC 語法 & #41;和處理傳回碼和輸出參數 & #40; OLE DB & #41;](../../../relational-databases/native-client-ole-db-how-to/results/execute-stored-procedure-with-rpc-and-process-output.md).  
  
### <a name="transact-sql-execute-statement"></a>Transact-SQL EXECUTE 陳述式  
 ODBC CALL 逸出序列和 RPC 逸出序列是慣用的方法，可以呼叫預存程序而非[EXECUTE](../../../t-sql/language-elements/execute-transact-sql.md)陳述式。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者所使用的 RPC 機制[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]來最佳化命令處理。 此 RPC 通訊協定會排除在伺服器上完成的許多參數處理與陳述式剖析，藉以增加效能。  
  
 這是範例[!INCLUDE[tsql](../../../includes/tsql-md.md)] **EXECUTE**陳述式：  
  
```  
EXECUTE SalesByCategory 'Produce', '1995'  
```  
  
## <a name="see-also"></a>另請參閱  
 [預存程序](../../../relational-databases/native-client/ole-db/stored-procedures.md)  
  
  
