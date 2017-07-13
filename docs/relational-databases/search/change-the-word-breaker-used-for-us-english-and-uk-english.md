---
title: "變更用於美式英文與英式英文的斷詞工具 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-search
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 6b5d2177-db98-47f5-b32e-4b80a2f74ffe
caps.latest.revision: 10
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: HT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: be3d7e956f6ed89f14fc63c36d97974cc9218933
ms.contentlocale: zh-tw
ms.lasthandoff: 07/10/2017

---
<a id="change-the-word-breaker-used-for-us-english-and-uk-english" class="xliff"></a>

# 變更用於美式英文與英式英文的斷詞工具
  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 會安裝適用於英文的新版 (14.0.4999.1038 版) 斷詞工具和字幹分析器，並取代這些舊版元件 (12.0.6828.0 版)。 如需新元件行為變更的詳細資訊，請參閱 [全文檢索搜尋的行為變更](http://msdn.microsoft.com/library/573444e8-51bc-4f3d-9813-0037d2e13b8f)。 本主題描述的是如何從新版元件切換成舊版，或從舊版切換回新版。 若為叢集安裝，就應該在所有主要和被動節點上進行這些變更。  
  
 舊版 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 使用了由美式英文 (LCID 1033) 和英式英文 (LCID 2057) 之不同 CLSID 所代表的不同斷詞工具。 在這個版本中，這兩個 LCID 都使用具有相同 CLSID 的相同元件，如下表所示：  
  
|LCID|舊版所安裝的斷詞工具<br /><br /> 12.0.6828.0 版|舊版所安裝的字幹分析器|這個版本所安裝的斷詞工具<br /><br /> 14.0.4999.1038 版|這個版本所安裝的字幹分析器|  
|----------|-------------------------------------------------------------------------|--------------------------------------------|-----------------------------------------------------------------------|---------------------------------------|  
|1033<br />(美式英文)|188D6CC5-CB03-4C01-912E-47D21295D77E|EEED4C20-7F1B-11CE-BE57-00AA0051FE20|9faed859-0b30-4434-ae65-412e14a16fb8|e1e5ef84-c4a6-4e50-8188-99aef3de2659|  
|2057<br />(英式英文)|173C97E2-AEBE-437C-9445-01B237ABF2F6|D99F7670-7F1A-11CE-BE57-00AA0051FE20|9faed859-0b30-4434-ae65-412e14a16fb8|e1e5ef84-c4a6-4e50-8188-99aef3de2659|  
  
 本主題所描述的元件是安裝在 `MSSQL\Binn` 執行個體之 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料夾中的 DLL 檔案。 完整路徑通常是 `C:\Program Files\Microsoft SQL Server\<instance>\MSSQL\Binn`。  
  
 如需斷詞工具與字幹分析器的詳細資訊，請參閱 [設定及管理搜尋的斷詞工具與字幹分析器](../../relational-databases/search/configure-and-manage-word-breakers-and-stemmers-for-search.md)。  
  
<a id="switching-from-the-current-english-word-breaker-to-the-previous-english-word-breakers" class="xliff"></a>

## 從目前的英文斷詞工具切換成先前的英文斷詞工具  
  
<a id="to-switch-from-the-current-version-of-the-us-english-word-breaker-to-the-previous-version" class="xliff"></a>

#### 若要從目前版本的美式英文斷詞工具切換成舊版  
  
1.  在登錄中，巡覽至下列節點：**HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\\<執行個體根目錄\>\MSSearch\CLSID**。  
  
2.  使用下列步驟，針對 LCID 1033 的舊版美式英文斷詞工具和字幹分析器介面加入 COM ClassID 的新機碼：  
  
    1.  針對先前的斷詞工具，加入含有 **{188D6CC5-CB03-4C01-912E-47D21295D77E}** 值的新機碼。  
  
    2.  將該機碼值的 (預設) 資料更新為 **langwrbk.dll**。  
  
    3.  針對先前的字幹分析器，加入含有 **{EEED4C20-7F1B-11CE-BE57-00AA0051FE20}** 值的新機碼。  
  
    4.  將該機碼值的 (預設) 資料更新為 **infosoft.dll**。  
  
3.  在登錄中，巡覽至下列節點：**HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\\<執行個體根目錄\>\MSSearch\Language\enu**。  
  
4.  將 **WBreakerClass** 機碼值更新為 **{188D6CC5-CB03-4C01-912E-47D21295D77E}**。  
  
5.  將 **StemmerClass** 機碼值更新為 **{EEED4C20-7F1B-11CE-BE57-00AA0051FE20}**。  
  
6.  重新啟動 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
<a id="to-switch-from-the-current-version-of-the-uk-english-word-breaker-to-the-previous-version" class="xliff"></a>

#### 若要從目前版本的英式英文斷詞工具切換成舊版  
  
1.  在登錄中，巡覽至下列節點：**HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\\<執行個體根目錄\>\MSSearch\CLSID**。  
  
2.  使用下列步驟，針對 LCID 2057 的先前英式英文斷詞工具和字幹分析器介面加入 COM ClassID 的新機碼：  
  
    1.  針對先前的斷詞工具，加入含有 **{173C97E2-AEBE-437C-9445-01B237ABF2F6}** 值的新機碼。  
  
    2.  將該機碼值的 (預設) 資料更新為 **langwrbk.dll**。  
  
    3.  針對先前的字幹分析器，加入含有 **{D99F7670-7F1A-11CE-BE57-00AA0051FE20}** 值的新機碼。  
  
    4.  將該機碼值的 (預設) 資料更新為 **infosoft.dll**。  
  
3.  在登錄中，巡覽至下列節點：**HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\\<執行個體根目錄\>\MSSearch\Language\eng**。  
  
4.  將 **WBreakerClass** 機碼值更新為 **{173C97E2-AEBE-437C-9445-01B237ABF2F6}**。  
  
5.  將 **StemmerClass** 機碼值更新為 **{D99F7670-7F1A-11CE-BE57-00AA0051FE20}**。  
  
6.  重新啟動 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
<a id="switching-back-from-the-previous-english-word-breakers-to-the-current-english-word-breaker" class="xliff"></a>

## 從先前的英文斷詞工具切換回目前的英文斷詞工具  
  
<a id="to-switch-back-from-the-previous-version-of-the-us-english-word-breaker-to-the-current-version" class="xliff"></a>

#### 若要從舊版的美式英文斷詞工具切換回目前版本  
  
1.  在登錄中，巡覽至下列節點：**HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\\<執行個體根目錄\>\MSSearch\CLSID**。  
  
2.  如果下列機碼不存在，請使用下列步驟，針對 LCID 1033 的目前美式英文斷詞工具和字幹分析器介面加入 COM ClassID 的新機碼：  
  
    1.  針對目前的斷詞工具，加入含有 **{9faed859-0b30-4434-ae65-412e14a16fb8}** 值的新機碼。  
  
    2.  將該機碼值的 (預設) 資料更新為 **MsWb7.dll**。  
  
    3.  針對目前的字幹分析器，加入含有 **{e1e5ef84-c4a6-4e50-8188-99aef3de2659}** 值的新機碼。  
  
    4.  將該機碼值的 (預設) 資料更新為 **MsWb7.dll**。  
  
3.  在登錄中，巡覽至下列節點：**HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\\<執行個體根目錄\>\MSSearch\Language\eng**。  
  
4.  將 **WBreakerClass** 機碼值更新為 **{9faed859-0b30-4434-ae65-412e14a16fb8}**。  
  
5.  將 **StemmerClass** 機碼值更新為 **{e1e5ef84-c4a6-4e50-8188-99aef3de2659}**。  
  
6.  重新啟動 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
<a id="to-switch-back-from-the-previous-version-of-the-uk-english-word-breaker-to-the-current-version" class="xliff"></a>

#### 若要從舊版的英式英文斷詞工具切換回目前版本  
  
1.  在登錄中，巡覽至下列節點：**HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\\<執行個體根目錄\>\MSSearch\CLSID**。  
  
2.  如果下列機碼不存在，請使用下列步驟，針對 LCID 2057 的目前英式英文斷詞工具和字幹分析器介面加入 COM ClassID 的新機碼：  
  
    1.  針對目前的斷詞工具，加入含有 **{9faed859-0b30-4434-ae65-412e14a16fb8}** 值的新機碼。  
  
    2.  將該機碼值的 (預設) 資料更新為 **MsWb7.dll**。  
  
    3.  針對目前的字幹分析器，加入含有 **{e1e5ef84-c4a6-4e50-8188-99aef3de2659}** 值的新機碼。  
  
    4.  將該機碼值的 (預設) 資料更新為 **MsWb7.dll**。  
  
3.  在登錄中，巡覽至下列節點：**HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\\<執行個體根目錄\>\MSSearch\Language\eng**。  
  
4.  將 **WBreakerClass** 機碼值更新為 **{9faed859-0b30-4434-ae65-412e14a16fb8}**。  
  
5.  將 **StemmerClass** 機碼值更新為 **{e1e5ef84-c4a6-4e50-8188-99aef3de2659}**。  
  
6.  重新啟動 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
<a id="see-also" class="xliff"></a>

## 另請參閱  
 [將搜索所使用的斷詞工具還原為舊版](../../relational-databases/search/revert-the-word-breakers-used-by-search-to-the-previous-version.md)   
 [全文檢索搜尋的行為變更](http://msdn.microsoft.com/library/573444e8-51bc-4f3d-9813-0037d2e13b8f)  
  
  
