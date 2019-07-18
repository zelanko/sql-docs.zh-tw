---
title: CREATE ACTION 陳述式 (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: b723a706521b24c9aa216c46f617d8ff94997137
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
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
 用戶端應用程式可以建立和執行不安全的動作；用戶端應用程式也可以使用不安全的函數。 若要避免這些情況下，使用**Safety**屬性。 如需詳細資訊，請參閱＜安全性選項屬性＞。  
  
> [!NOTE]  
>  包含此陳述式是為了回溯相容性 (Backward Compatibility) 的需要。 新動作[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]，例如鑽研或報表動作，不支援。  
  
## <a name="action-types"></a>動作類型  
 下表描述不同類型的可用動作的[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]。  
  
|動作類型|描述|  
|-----------------|-----------------|  
|**URL**|傳回的動作字串是 URL，應使用網際網路瀏覽器開啟。<br /><br /> 注意:如果此動作不是以開頭`https://`或`https://`，此動作會在瀏覽器無法使用除非**SafetyOptions**設定為**DBPROPVAL_MSMD_SAFETY_OPTIONS_ALLOW_ALL**。|  
|**HTML**|傳回的動作字串是 HTML 指令碼。 應將此字串儲存至檔案，而且應使用網際網路瀏覽器來轉譯此檔案。 在此情況下，可能會將整個指令碼視為已產生 HTML 的一部分執行。|  
|**陳述式**|傳回的動作字串是需要藉由設定執行的陳述式**ICommand::SetText**方法的字串，並呼叫命令物件**icommand:: Execute**方法。 如果未能成功執行此命令，會傳回錯誤。|  
|**資料集**|傳回的動作字串是必須藉由設定執行 MDX 陳述式**ICommand::SetText**方法的字串，並呼叫命令物件**icommand:: Execute**方法。 要求的介面識別碼 (IID) 應**IDataset**。 如果已建立資料集，此命令就能成功執行。 用戶端應用程式應該允許使用者瀏覽傳回的資料集。|  
|**資料列集**|類似於**資料集**，而不是要求的 IID，但**IDataset**，用戶端應用程式應該詢問的 iid **IRowset**。 如果已建立資料列集，此命令就能成功執行。 用戶端應用程式應該允許使用者瀏覽傳回的資料列集。|  
|**命令列**|用戶端應用程式應執行此動作字串。 此字串是一個命令列。|  
|**專屬**|除非用戶端應用程式有自訂、非一般的特定動作，否則應用程式不應該顯示，也不該執行此動作。 除非用戶端應用程式明確提出要求上設定適當的限制不專屬動作傳回用戶端應用程式**APPLICATION_NAME**。|  
  
## <a name="invocation-types"></a>引動過程類型  
 下表描述 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 中可用的不同引動過程類型。 引動過程類型只由用戶端應用程式使用，可協助判定何時要叫用動作。 引動過程類型實際上不會決定動作的引動過程行為。  
  
|引動過程類型|描述|  
|---------------------|-----------------|  
|**互動式**|此動作應透過使用者互動，由用戶端應用程式叫用。|  
|**ON_OPEN**|此動作應在目標物件開啟時，由用戶端應用程式叫用。 目前未實作此引動過程類型。|  
|**BATCH**|此動作應在用戶端應用程式決定要在批次作業中叫用目標物件時，由用戶端應用程式叫用。 目前未實作此引動過程類型。|  
  
### <a name="scope"></a>`Scope`  
 每個動作是為特定 Cube 而定義，而且在該 Cube 中有唯一的名稱。 一個動作可有下表列出的其中一個範圍。  
  
 Cube 範圍  
 獨立於特定維度、 成員或儲存格的動作例如：「 啟動終端機模擬 as/400 生產系統 」。  
  
 維度範圍  
 此動作適用於特定維度。 這些動作不相依於層級或成員的特定選取項目。  
  
 層級範圍  
 此動作適用於特定維度層級。 這些動作不相依於該維度內成員的特定選取項目。  
  
 成員範圍  
 此動作適用於特定層級成員。  
  
 資料格範圍  
 此動作僅適用於特定資料格。  
  
 集合範圍  
 此動作僅適用於集合。 名稱 **ActionParameterSet**，已保留供動作的運算式內的應用程式。  
  
## <a name="see-also"></a>另請參閱  
 [MDX 資料定義陳述式&#40;MDX&#41;](../mdx/mdx-data-definition-statements-mdx.md)  
  
  
