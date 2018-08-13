---
title: 刪除資料使用 XML Updategram (SQLXML 4.0) |Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: sqlxml
ms.reviewer: ''
ms.suite: sql
ms.technology: xml
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- <after> block
- updategrams [SQLXML], deleting data
- <before> block
- mapping-schema attribute
- record deletions [SQLXML]
ms.assetid: 4fb116d7-7652-474a-a567-cb475a20765c
caps.latest.revision: 24
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017
ms.openlocfilehash: 462aae19c9c01ef4b4eb3cd4ccc01ddd6a3e07d3
ms.sourcegitcommit: 4cd008a77f456b35204989bbdd31db352716bbe6
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/06/2018
ms.locfileid: "39559138"
---
# <a name="deleting-data-using-xml-updategrams-sqlxml-40"></a>使用 XML Updategram 刪除資料 (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  當記錄執行個體中出現時，updategram 代表刪除作業**\<之前 >** 區塊中沒有對應記錄**\<之後 >** 區塊。 在此情況下，updategram 會刪除中的資料錄**\<之前 >** 從資料庫的區塊。  
  
 下列是刪除作業的 Updategram 格式：  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
  <updg:sync [mapping-schema="SampleSchema.xml"]  >  
   <updg:before>  
       <ElementName />  
      [<ElementName .../>... ]  
   </updg:before>  
    [<updg:after>  
    </updg:after>]  
  </updg:sync>  
</ROOT>  
```  
  
 您可以省略**\<之後 >** 標記如果 updategram 會執行刪除作業。 如果您未指定選擇性**對應結構描述**屬性， **\<項目名稱 >** 則 updategram 會對應至資料庫資料表與子元素或屬性對應到所指定資料表中的資料行。  
  
 如果在 updategram 中指定的項目會符合資料表中的多個資料列，或者不符合任何資料列，updategram 會傳回錯誤，並取消整個**\<同步 >** 區塊。 Updategram 中的元素一次只能刪除一個記錄。  
  
## <a name="examples"></a>範例  
 本章節中的範例會使用預設對應 (也就是說，Updategram 中不會指定任何對應結構描述)。 如需使用對應結構描述的 updategram 的範例，請參閱[在 Updategram 中指定註解式對應結構描述&#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/updategrams/specifying-an-annotated-mapping-schema-in-an-updategram-sqlxml-4-0.md)。  
  
 若要建立使用下列範例的實用範例，您必須符合指定的需求[如需執行 SQLXML 範例的需求](../../../relational-databases/sqlxml/requirements-for-running-sqlxml-examples.md)。  
  
### <a name="a-deleting-a-record-by-using-an-updategram"></a>A. 使用 Updategram 刪除記錄  
 下列 Updategram 會從 HumanResources.Shift 資料表刪除兩筆記錄。  
  
 在這些範例中，Updategram 不會指定對應結構描述。 因此 Updategram 會使用預設對應，其中元素的名稱會對應到資料表名稱，而屬性或子元素則會對應到資料行。  
  
 這個第一個 updategram 以屬性為中心和識別 （一天 Day-evening 和 Evening-night） 的兩個值班**\<之前 >** 區塊。 因為沒有任何對應的記錄**\<之後 >** 區塊中，這是刪除作業。  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
<updg:sync >  
  <updg:before>  
       <HumanResources.Shift ShiftID="4"  
                        Name="Day-Evening"  
                        StartTime="1900-01-01 11:00:00.000"  
                        EndTime="1900-01-01 19:00:00.000"  
                        ModifiedDate="2004-01-01 00:00:00.000" />  
       <HumanResources.Shift ShiftID="5"  
                        Name="Evening-Night"  
                        StartTime="1900-01-01 19:00:00.000"  
                        EndTime="1900-01-01 03:00:00.000"  
                        ModifiedDate="2004-01-01 00:00:00.000" />  
  </updg:before>  
  <updg:after>  
  </updg:after>  
</updg:sync>  
</ROOT>  
```  
  
##### <a name="to-test-the-updategram"></a>若要測試 Updategram  
  
1.  完整的範例 B （「 插入多筆記錄使用 updategram 」） 中[插入的資料使用 XML Updategram &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/updategrams/inserting-data-using-xml-updategrams-sqlxml-4-0.md)。  
  
2.  將上述的 updategram 複製到 [記事本]，並將它儲存為 Updategram-removeshifts.xml 相同的資料夾中，用來完成 （「 插入多筆記錄使用 updategram 」） 中[插入的資料使用 XML Updategram &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/updategrams/inserting-data-using-xml-updategrams-sqlxml-4-0.md).  
  
3.  建立及使用 SQLXML 4.0 測試指令碼 (Sqlxml4test.vbs) 以執行 Updategram。  
  
     如需詳細資訊，請參閱 <<c0> [ 使用 ADO 執行 SQLXML 4.0 查詢](../../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)。  
  
## <a name="see-also"></a>另請參閱  
 [Updategram 安全性考量&#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/security/updategram-security-considerations-sqlxml-4-0.md)  
  
  
