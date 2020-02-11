---
title: CREATE ACTION 語句（MDX） |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: b723a706521b24c9aa216c46f617d8ff94997137
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68098547"
---
# <a name="mdx-data-definition---create-action"></a>MDX 資料定義 - CREATE ACTION


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
 用戶端應用程式可以建立和執行不安全的動作；用戶端應用程式也可以使用不安全的函數。 若要避免這些情況，請使用 [**安全性選項**] 屬性。 如需詳細資訊，請參閱＜安全性選項屬性＞。  
  
> [!NOTE]  
>  包含此陳述式是為了回溯相容性 (Backward Compatibility) 的需要。 不支援新[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]的動作，例如「鑽取」或「報表」動作。  
  
## <a name="action-types"></a>動作類型  
 下表描述中[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]可用的各種動作類型。  
  
|動作類型|描述|  
|-----------------|-----------------|  
|**連結**|傳回的動作字串是 URL，應使用網際網路瀏覽器開啟。<br /><br /> 注意：如果此動作的開頭不是`https://`或`https://`，瀏覽器將無法使用此動作，除非**SafetyOptions**設為**DBPROPVAL_MSMD_SAFETY_OPTIONS_ALLOW_ALL**。|  
|**HTML**|傳回的動作字串是 HTML 指令碼。 應將此字串儲存至檔案，而且應使用網際網路瀏覽器來轉譯此檔案。 在此情況下，可能會將整個指令碼視為已產生 HTML 的一部分執行。|  
|**句**|傳回的動作字串是一種語句，必須藉由將 command 物件的**ICommand：： SetText**方法設定為字串，並呼叫**ICommand：： Execute**方法來執行。 如果未能成功執行此命令，會傳回錯誤。|  
|**集中**|傳回的動作字串是 MDX 語句，必須藉由將 command 物件的**ICommand：： SetText**方法設定為字串，並呼叫**ICommand：： Execute**方法來執行。 要求的介面識別碼（IID）應為**IDataset**。 如果已建立資料集，此命令就能成功執行。 用戶端應用程式應該允許使用者瀏覽傳回的資料集。|  
|**資料列集**|與**DATASET**相似，但用戶端應用程式應該要求**IRowset**的 iid，而不是要求**IDataset**的 iid。 如果已建立資料列集，此命令就能成功執行。 用戶端應用程式應該允許使用者瀏覽傳回的資料列集。|  
|**命令列**|用戶端應用程式應執行此動作字串。 此字串是一個命令列。|  
|**專屬**|除非用戶端應用程式有自訂、非一般的特定動作，否則應用程式不應該顯示，也不該執行此動作。 除非用戶端應用程式藉由在**APPLICATION_NAME**上設定適當的限制，明確要求，否則不會將專屬動作傳回給用戶端應用程式。|  
  
## <a name="invocation-types"></a>引動過程類型  
 下表描述 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 中可用的不同引動過程類型。 引動過程類型只由用戶端應用程式使用，可協助判定何時要叫用動作。 引動過程類型實際上不會決定動作的引動過程行為。  
  
|引動過程類型|描述|  
|---------------------|-----------------|  
|**互動式**|此動作應透過使用者互動，由用戶端應用程式叫用。|  
|**ON_OPEN**|此動作應在目標物件開啟時，由用戶端應用程式叫用。 目前未實作此引動過程類型。|  
|**成批**|此動作應在用戶端應用程式決定要在批次作業中叫用目標物件時，由用戶端應用程式叫用。 目前未實作此引動過程類型。|  
  
### <a name="scope"></a>影響範圍  
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
 此動作僅適用於集合。 名稱**ActionParameterSet**是保留供應用程式在動作的運算式內使用。  
  
## <a name="see-also"></a>另請參閱  
 [Mdx 資料定義語句 &#40;MDX&#41;](../mdx/mdx-data-definition-statements-mdx.md)  
  
  
