---
title: DISCOVER_COMMANDS 資料列集 |Microsoft 文件
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- DISCOVER_COMMANDS rowset
ms.assetid: d228f265-05d9-4d2c-a622-44c73eab7a71
caps.latest.revision: 14
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 14c4eb9ac8fe63422ee29f5880a8a5f1eb6329bf
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36034664"
---
# <a name="discovercommands-rowset"></a>DISCOVER_COMMANDS 資料列集
  提供在伺服器上已開啟的連接中，目前執行或是上次執行的命令之資源使用量與活動資訊。  
  
 **適用於：** 表格式模型、 多維度模型  
  
## <a name="rowset-columns"></a>資料列集資料行  
 `DISCOVER_COMMANDS`資料列集包含下列資料行。  
  
|資料行名稱|類型指標|限制|描述|  
|-----------------|--------------------|-----------------|-----------------|  
|`SESSION_SPID`|`DBTYPE_I4`|是|工作階段識別碼。|  
|`SESSION_COMMAND_COUNT`|`DBTYPE_I4`||工作階段開始之後所執行的命令數目。|  
|`COMMAND_START_TIME`|`DBTYPE_DBTIMESTAMP`||上一個命令啟動的日期與時間，以伺服器的 UTC 時間表示。|  
|`COMMAND_ELAPSED_TIME_MS`|`DBTYPE_I8`||命令開始以後所經過的時間 (以毫秒為單位)。|  
|`COMMAND_CPU_TIME_MS`|`DBTYPE_I8`||命令執行開始以後，命令所耗用的 CPU 時間 (以毫秒為單位)。|  
|`COMMAND_READS`|`DBTYPE_I8`||命令開始以後，磁碟讀取的累積數目。|  
|`COMMAND_READ_KB`|`DBTYPE_I8`||命令開始以後，從磁碟讀取的資料累積值 (以 KB 為單位)。|  
|`COMMAND_WRITES`|`DBTYPE_I8`||命令開始以後，磁碟寫入的累積數目。|  
|`COMMAND_WRITE_KB`|`DBTYPE_I8`||命令開始以後，寫入磁碟的資料累積值 (以 KB 為單位)。|  
|`COMMAND_TEXT`|`DBTYPE_WSTR`||命令文字。|  
|`COMMAND_END_TIME`|`DBTYPE_DBTIMESTAMP`||當命令完成其執行時，伺服器的 UTC 日期與時間。|  
  
 這個結構描述資料列集並未排序。  
  
## <a name="using-adomdnet-to-return-the-rowset"></a>使用 ADOMD.NET 傳回資料列集  
 使用 ADOMD.NET 和結構描述資料列集來擷取中繼資料時，您可以使用 GUID 或字串，在 GetSchemaDataSet 方法中參考結構描述資料列集物件。 如需詳細資訊，請參閱 [Working with Schema Rowsets in ADOMD.NET](../../../relational-databases/native-client-ole-db-rowsets/rowsets.md)。  
  
 下表將提供可識別此資料列集的 GUID 和字串值。  
  
|引數|ReplTest1|  
|--------------|-----------|  
|GUID|a07ccd34-8148-11d0-87bb-00c04fc33942|  
|ADOMDNAME|命令|  
  
## <a name="see-also"></a>另請參閱  
 [XML for Analysis 結構描述資料列集](xml-for-analysis-schema-rowsets.md)  
  
  