---
title: 參數化命令的操作 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- data shaping [ADO], parameterized commands
- parameterized commands [ADO]
ms.assetid: 4fae0d54-83b6-4ead-99cc-bcf532daa121
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e7d4399a8cf279ed2283061fff9064ffcc1adfba
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "67924730"
---
# <a name="operation-of-parameterized-commands"></a>參數化命令的作業
如果您使用的是大型子**記錄集**，特別是與父**記錄集**的大小相比較，但只需要存取一些子章節，您可能會發現使用參數化命令會更有效率。  
  
 *非參數化命令*會同時抓取整個父系和子**記錄集**、將章節資料行附加至父系，然後針對每個父資料列指派相關子章節的參考。  
  
 *參數化命令*會抓取整個父**記錄集**，但只有在存取章節資料行時，才會抓取章節**記錄集**。 這項抓取策略的差異可能會產生顯著的效能優勢。  
  
 例如，您可以指定下列各項：  
  
```  
SHAPE {SELECT * FROM customer}   
   APPEND ({SELECT * FROM orders WHERE cust_id = ?}   
   RELATE cust_id TO PARAMETER 0)  
```  
  
 父系和子資料工作表的資料行名稱為 common， *cust_id*。 *子命令*具有「？」預留位置，其中的「關聯」子句會參考它（也就是「.。。參數 0 "）。  
  
> [!NOTE]
>  PARAMETER 子句僅適用于 shape 命令語法。 它不會與 ADO[參數](../../../ado/reference/ado-api/parameter-object.md)物件或[Parameters](../../../ado/reference/ado-api/parameters-collection-ado.md)集合相關聯。  
  
 執行參數化圖形命令時，會發生下列情況：  
  
1.  *父-命令*會執行，並從 Customers 資料表傳回父**記錄集**。  
  
2.  [章節] 資料行會附加至父**記錄集**。  
  
3.  存取父資料列的 [章節] 資料行時，會使用 customer 的值來執行*子命令*。 cust_id 做為參數的值。  
  
4.  在步驟3中建立之資料提供者資料列集內的所有資料列都會用來填入子**記錄集**。 在此範例中，這是 Orders 資料表中的所有資料列，其中 cust_id 等於 customer 的值。 cust_id。 根據預設，子**記錄集**的會在用戶端上快取，直到父**記錄集**的所有參考都已釋放為止。 若要變更此行為，請將**記錄集**[動態屬性](../../../ado/reference/ado-api/ado-dynamic-property-index.md)快取**子資料列**設定為**False**。  
  
5.  所抓取之子資料列的參考（也就是子**記錄集**的章節）會放在父**記錄集**目前資料列的 [章節] 資料行中。  
  
6.  存取另一個資料列的章節資料行時，會重複步驟3-5。  
  
 [快取**子資料列**] 動態屬性預設會設定為 [ **True** ]。 快取行為會依據查詢的參數值而有所不同。 在具有單一參數的查詢中，指定參數值的子**記錄集**會在具有該值的子系的要求之間快取。 下列程式碼將示範此作業：  
  
```  
SCmd = "SHAPE {select * from customer} " & _  
         "APPEND({select * from orders where cust_id = ?} " & _  
         "RELATE cust_id TO PARAMETER 0) AS chpCustOrder"  
Rst1.Open sCmd, Cnn1  
Set RstChild = Rst1("chpCustOrder").Value  
Rst1.MoveNext      ' Next cust_id passed to Param 0, & new rs fetched   
                   ' into RstChild.  
Rst1.MovePrevious  ' RstChild now holds cached rs, saving round trip.  
```  
  
 在具有兩個或多個參數的查詢中，只有在所有參數值都符合快取的值時，才會使用快取的子系。  
  
## <a name="parameterized-commands-and-complex-parent-child-relations"></a>參數化命令和複雜的父子式關聯  
 除了使用參數化命令來改善等聯結類型階層的效能之外，參數化命令也可以用來支援更複雜的父子關聯性。 例如，假設有一個小聯盟資料庫包含兩個數據表：一個由小組（team_id、team_name）和其他遊戲（日期、home_team、visiting_team）組成。  
  
 使用非參數化階層時，無法建立小組和遊戲資料表的關聯性，因為每個小組的子**記錄集**都包含完整的排程。 您可以建立包含主排程或道路排程的章節，但不能兩者都有。 這是因為「關聯」子句會限制您對表單的父子式關聯性（pc1 = cc1）和（pc2 = pc2）。 因此，如果您的命令包含「關聯 team_id 至 home_team，team_id visiting_team」，您就只會收到小組自行播放的遊戲。 您想要的是 "（team_id = home_team）或（team_id = visiting_team）"，但圖形提供者不支援或子句。  
  
 若要取得想要的結果，您可以使用參數化命令。 例如：  
  
```  
SHAPE {SELECT * FROM teams}   
APPEND ({SELECT * FROM games WHERE home_team = ? OR visiting_team = ?}   
        RELATE team_id TO PARAMETER 0,   
               team_id TO PARAMETER 1)   
```  
  
 這個範例會利用 SQL WHERE 子句的更大彈性來取得您所需的結果。  
  
> [!NOTE]
>  使用 WHERE 子句時，參數無法使用 text、Ntext 和 image 的 SQL 資料類型，否則會產生包含下列描述的錯誤： `Invalid operator for data type`。  
  
## <a name="see-also"></a>另請參閱  
 [資料成形範例](../../../ado/guide/data/data-shaping-example.md)   
 [正式圖形文法](../../../ado/guide/data/formal-shape-grammar.md)   
 [一般 Shape 命令](../../../ado/guide/data/shape-commands-in-general.md)
