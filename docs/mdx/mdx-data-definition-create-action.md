---
title: "CREATE ACTION 陳述式 (MDX) |Microsoft 文件"
ms.custom: 
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- CREATE ACTION
- Action
- CREATE
- CREATE_ACTION
dev_langs: kbMDX
helpviewer_keywords:
- invocation types [MDX]
- dimensions [Analysis Services], actions
- CREATE ACTION statement
- cubes [Analysis Services], actions
- actions [MDX]
- hierarchies [Analysis Services], actions
ms.assetid: 0419f349-ece2-42ba-8552-a1023f268a41
caps.latest.revision: "36"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: d065e9163a85e366dbe51f964058e8627e278be7
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/27/2017
---
# <a name="mdx-data-definition---create-action"></a>MDX 資料定義-建立動作
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  建立與 Cube、維度、階層或從屬物件關聯的動作。  
  
## <a name="syntax"></a>語法  
  
```  
  
CREATE ACTION CURRENTCUBE | Cube_Name  
   .Action_Name <action body>  
<action body> ::=   
FOR   
        CUBE   
    | Hierarchy_Name [MEMBERS]   
    | Level_Name [MEMBERS]   
    | CELLS   
    | SET }   
      AS 'MDX_Expression'   
        [, TYPE = '  
              { URL   
            | HTML   
            | STATEMENT   
               | DATASET   
            | ROWSET   
            | COMMANDLINE   
               | PROPRIETARY }   
         ']  
   [ , INVOCATION = 'INTERACTIVE | ON_OPEN | BATCH ' ]  
   [ , APPLICATION = String_Expression ]  
   [ , DESCRIPTION = String_Expression ]  
   [ , CAPTION = 'MDX_Expression' ]  
```  
  
## <a name="arguments"></a>引數  
 *Cube_Name*  
 提供 Cube 名稱的有效字串。  
  
 *Action_ 名稱*  
 提供將要建立之動作名稱的有效字串。  
  
 *Hierarchy_ 名稱*  
 提供階層名稱的有效字串。  
  
 *Level_ 名稱*  
 提供層級名稱的有效字串。  
  
 *Member_ 名稱*  
 提供成員名稱或成員索引鍵的有效字串。  
  
 *MDX_Expression*  
 有效的 MDX 運算式。  
  
 *String_Expression*  
 有效的字串運算式。  
  
## <a name="remarks"></a>備註  
 用戶端應用程式可以建立和執行不安全的動作；用戶端應用程式也可以使用不安全的函數。 若要避免發生這些情況下，使用**Safety Options**屬性。 如需詳細資訊，請參閱＜安全性選項屬性＞。  
  
> [!NOTE]  
>  包含此陳述式是為了回溯相容性 (Backward Compatibility) 的需要。 新動作[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]，不支援鑽研或報表動作，例如。  
  
## <a name="action-types"></a>動作類型  
 下表說明不同類型中可用動作的[!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]。  
  
|動作類型|Description|  
|-----------------|-----------------|  
|**URL**|傳回的動作字串是 URL，應使用網際網路瀏覽器開啟。<br /><br /> 注意： 如果此動作不是以開頭`http://`或`https://`，此動作將無法用於瀏覽器除非**SafetyOptions**設為**與 DBPROPVAL_MSMD_SAFETY_OPTIONS_ALLOW_ALL**。|  
|**HTML**|傳回的動作字串是 HTML 指令碼。 應將此字串儲存至檔案，而且應使用網際網路瀏覽器來轉譯此檔案。 在此情況下，可能會將整個指令碼視為已產生 HTML 的一部分執行。|  
|**陳述式**|傳回的動作字串是需要藉由設定執行的陳述式**ICommand::SetText**命令物件的字串，並呼叫的方法**icommand:: Execute**方法。 如果未能成功執行此命令，會傳回錯誤。|  
|**資料集**|傳回的動作字串是必須藉由設定執行 MDX 陳述式**ICommand::SetText**命令物件的字串，並呼叫的方法**icommand:: Execute**方法。 要求的介面識別碼 (IID) 應為**IDataset**。 如果已建立資料集，此命令就能成功執行。 用戶端應用程式應該允許使用者瀏覽傳回的資料集。|  
|**資料列集**|類似於**資料集**，但不要求的 IID **IDataset**，用戶端應用程式應該要求的 iid **IRowset**。 如果已建立資料列集，此命令就能成功執行。 用戶端應用程式應該允許使用者瀏覽傳回的資料列集。|  
|**命令列**|用戶端應用程式應執行此動作字串。 此字串是一個命令列。|  
|**專屬**|除非用戶端應用程式有自訂、非一般的特定動作，否則應用程式不應該顯示，也不該執行此動作。 專屬動作不會傳回給用戶端應用程式用戶端應用程式，明確提出要求上設定適當限制，除非**APPLICATION_NAME**。|  
  
## <a name="invocation-types"></a>引動過程類型  
 下表描述 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 中可用的不同引動過程類型。 引動過程類型只由用戶端應用程式使用，可協助判定何時要叫用動作。 引動過程類型實際上不會決定動作的引動過程行為。  
  
|引動過程類型|Description|  
|---------------------|-----------------|  
|**互動式**|此動作應透過使用者互動，由用戶端應用程式叫用。|  
|**ON_OPEN**|此動作應在目標物件開啟時，由用戶端應用程式叫用。 目前未實作此引動過程類型。|  
|**批次**|此動作應在用戶端應用程式決定要在批次作業中叫用目標物件時，由用戶端應用程式叫用。 目前未實作此引動過程類型。|  
  
### <a name="scope"></a>範圍。  
 每個動作是為特定 Cube 而定義，而且在該 Cube 中有唯一的名稱。 一個動作可有下表列出的其中一個範圍。  
  
 Cube 範圍  
 獨立於特定維度、成員或資料格集的動作；例如：「啟動 AS/400  生產系統的終端機模擬」。  
  
 維度範圍  
 此動作適用於特定維度。 這些動作不相依於層級或成員的特定選取項目。  
  
 層級範圍  
 此動作適用於特定維度層級。 這些動作不相依於該維度內成員的特定選取項目。  
  
 成員範圍  
 此動作適用於特定層級成員。  
  
 資料格範圍  
 此動作僅適用於特定資料格。  
  
 集合範圍  
 此動作僅適用於集合。 「 名稱 」， **ActionParameterSet**，已保留供動作的運算式內的應用程式。  
  
## <a name="see-also"></a>請參閱  
 [MDX 資料定義陳述式 &#40;MDX &#41;](../mdx/mdx-data-definition-statements-mdx.md)  
  
  
