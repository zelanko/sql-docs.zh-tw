---
title: rskeymgmt 公用程式 (SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 03/20/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.component: tools
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- report servers [Reporting Services], encryption
- joining report server instances [SQL Server]
- report server scale-out deployments [Reporting Services]
- cryptography [Reporting Services]
- multiple report server instances
- command prompt utilities [Reporting Services]
- report servers [Reporting Services], scale-out deployments
- encryption [Reporting Services]
- rskeymgmt utility
- scale-out deployments [Reporting Services]
ms.assetid: 53f1318d-bd2d-4c08-b19f-c8b698b5b3d3
caps.latest.revision: 56
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: c2bdcd2610eb4a4c6d351868a8fbb7aac9a44bf7
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="rskeymgmt-utility-ssrs"></a>rskeymgmt 公用程式 (SSRS)
  擷取、還原、建立和刪除「用來保護機密報表伺服器資料，以免遭到未獲授權的存取」之對稱金鑰。 另外，這個公用程式也用來將報表伺服器執行個體聯結在向外延展部署中。 「報表伺服器向外延展部署」是指共用單一報表伺服器資料庫的多個報表伺服器執行個體。  
  
## <a name="syntax"></a>語法  
  
```  
  
rskeymgmt {-?}  
{–eextract}  
{–aapply}  
{-ddeleteall}  
{–srecreatekey}  
{–rremoveinstancekey}  
{-jjoinfarm}  
{-iinstance}  
{-ffile}  
{-pencryptionpassword}  
{-mremotecomputer}  
{-ninstancenameofremotecomputer}  
{-uadministratoruseraccount}  
{-vadministratorpassword}  
{-ttrace}  
```  
  
## <a name="arguments"></a>引數  
 **-?**  
 顯示 **rskeymgmt** 引數的語法。  
  
 **-e**  
 擷取「用來加密和解密報表伺服器執行個體的資料，以便將它複製到檔案中」之對稱金鑰。  
  
 此引數沒有取得值。 不過，命令列必須包括其他引數，才能完成擷取作業。 您必須指定的引數包括 **-f** 和 **-p**。  
  
 **-a**  
 利用密碼保護的備份檔所提供之副本來取代現有的對稱金鑰。 這會更新對稱金鑰的所有執行個體。  
  
 此引數沒有取得值。 不過，命令列必須包括其他引數，才能選取要套用的金鑰所在的檔案。 您可以指定的引數包括 **-f** 和 **-p**。  
  
 **-d**  
 刪除所有對稱金鑰執行個體及報表伺服器資庫中所有已加密的資料。 此引數沒有取得值。  
  
 **-s**  
 產生新的對稱金鑰，以及利用新的金鑰來重新加密所有已加密的內容。 這會重新產生對稱金鑰的所有執行個體。  
  
 **-j**  
 設定遠端報表伺服器執行個體來共用本機報表伺服器執行個體所用的報表伺服器資料庫。  
  
 **-r**  <安裝識別碼>  
 移除特定報表伺服器執行個體的對稱金鑰資訊，因而從向外延展部署中移除報表伺服器。 <安裝識別碼> 是一個 GUID 值，可在 RSReportserver.config 檔中找到它。  
  
 **-f**  <檔案>  
 指定儲存了對稱金鑰備份副本之檔案的完整路徑。  
  
 若為 **rskeymgmt -e**，對稱金鑰會寫入您指定的檔案中。  
  
 若為 **rskeymgmt -a**，便會將檔案中所儲存的對稱金鑰值套用在報表伺服器執行個體上。  
  
 **-p** <密碼>  
 ( **-f**需要這個引數) 指定用來備份或套用對稱金鑰的密碼。 這個值不能空白。  
  
 **-i**  
 指定本機報表伺服器執行個體。 如果您將報表伺服器安裝在預設的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體上，這個引數即為選擇性 ( **-i** 的預設值是 MSSQLSERVER)。 若您將報表伺服器安裝成具名執行個體，就需要 **-i** 。  
  
 **-m**  
 指定要聯結至報表伺服器向外延展部署中，主控報表伺服器執行個體的遠端電腦名稱。 請使用在網路中用來識別這部電腦的名稱。  
  
 **-n**  
 指定遠端電腦中之報表伺服器執行個體的名稱。 如果您將報表伺服器安裝在預設的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體上，這個引數即為選擇性 ( **-n** 的預設值是 MSSQLSERVER)。 若您將報表伺服器安裝成具名執行個體，則需要 **-n**。  
  
 **-u**  <使用者帳戶>  
 指定要聯結至向外延展部署中之遠端電腦的管理員帳戶。 如果未指定帳戶，就會使用目前使用者的認證。  
  
 **-v**  <密碼>  
 ( **-u**需要這個引數) 指定要聯結至向外延展部署中之遠端電腦的管理員帳戶密碼。  
  
 **-t**  <追蹤>  
 在追蹤記錄中，輸出錯誤訊息。 此引數沒有取得值。 如需詳細資訊，請參閱 [Report Server Service Trace Log](../../reporting-services/report-server/report-server-service-trace-log.md)。  
  
## <a name="permissions"></a>Permissions  
 您必須是執行這套工具的本機管理員，且您必須在主控報表伺服器之電腦的本機環境中執行它。 rskeymgmt 公用程式會使用本機報表伺服器 Windows 執行個體 (這個公用程式無法連接報表伺服器 Windows 服務的遠端執行個體，因此，您無法利用它來管理遠端報表伺服器執行個體的加密金鑰)。  
  
> [!NOTE]  
>  如果您使用 **-u** 和 **-v** 引數，請務必指定對遠端電腦具有管理員權限的帳戶。  
  
## <a name="examples"></a>範例  
 下列範例說明 **rskeymgmt**的使用方式。 下列範例會顯示如何擷取、還原和刪除加密金鑰，以及如何設定報表伺服器的向外延展部署。  
  
#### <a name="extracting-encryption-keys"></a>擷取加密金鑰  
 這個範例會顯示如何建立加密金鑰的備份副本，以及將它儲存在磁碟片的密碼保護檔案中。 如果報表伺服器安裝成具名執行個體，請加入 **-i** 引數。  
  
```  
rskeymgmt -e -f a:\backupkey\keys -p <password>  
```  
  
#### <a name="restoring-encryption-keys"></a>還原加密金鑰  
 這個範例會顯示如何取代加密金鑰。 您必須指定金鑰備份副本的位置以及將檔案解除鎖定的密碼。  
  
```  
rskeymgmt -a -f a:\backupkey\keys -p <password>  
```  
  
#### <a name="deleting-encryption-keys-and-encrypted-content"></a>刪除加密金鑰和加密內容  
 這個範例會顯示如何刪除報表伺服器所儲存的所有加密金鑰。 如果您的安裝架構是一項報表伺服器向外延展部署，便會刪除部署所包含的所有報表伺服器執行個體的加密金鑰。 刪除加密金鑰也會刪除報表伺服器資料庫中任何現有的加密值。 如需加密內容的詳細資訊，請參閱[儲存加密的報表伺服器資料 &#40;SSRS 設定管理員&#41;](../../reporting-services/install-windows/ssrs-encryption-keys-store-encrypted-report-server-data.md)。  
  
```  
rskeymgmt -d  
```  
  
#### <a name="joining-a-remote-report-server-named-instance-to-a-scale-out-deployment"></a>將遠端報表伺服器具名執行個體聯結至向外延展部署中  
 這個範例會顯示如何將遠端電腦所安裝的報表伺服器執行個體加入報表伺服器向外延展部署中。 您必須在已設定成要使用共用資料庫的其中一部電腦中執行這個命令。 命令引數會指定要聯結至向外延展部署中的遠端報表伺服器執行個體。  
  
```  
rskeymgmt -j -m <remotecomputer> -n <namedreportserverinstance> -u <administratoraccount> -v <administratorpassword>  
```  
  
> [!NOTE]  
>  報表伺服器向外延展部署是指多個報表伺服器執行個體共用相同報表伺服器資料庫的部署模型。 對稱金鑰儲存在報表伺服器資料庫中的任何報表伺服器執行個體，都可以使用報表伺服器資料庫。 例如，如果報表伺服器資料庫包含三個報表伺服器執行個體的金鑰資訊，這三個執行個體都會被視為相同向外延展部署的成員。  
  
#### <a name="joining-report-server-instances-on-the-same-computer"></a>在相同電腦上聯結報表伺服器執行個體  
 您可以從安裝在相同電腦上的多個報表伺服器執行個體中建立向外延展部署。 如果您要聯結的報表伺服器執行個體是安裝在本機，請不要設定 **-u** 和 **-v** 引數。 只有當您從遠端電腦聯結執行個體時，才要使用 **-u** 和 **-v** 引數。 如果您指定這些引數，會出現下列錯誤：「使用者認證無法用於本機連接。」  
  
 下列範例說明使用多個本機執行個體建立向外延展部署的語法。 在這個範例中，\<**已初始化的執行個體**> 是已初始化為使用報表伺服器資料庫的執行個體名稱，\<**新的執行個體**> 是您要新增部署的執行個體名稱：  
  
```  
rskeymgmt -j -i <initializedinstance> -m <computer name> -n <newinstance>  
```  
  
#### <a name="removing-encryption-keys-for-a-single-report-server-in-a-scale-out-deployment"></a>移除向外延展部署中之單一報表伺服器的加密金鑰  
 這個範例會顯示如何在報表伺服器的向外延展部署中，移除單一報表伺服器的加密金鑰。 這些金鑰會從報表伺服器資料庫中移除。 移除報表伺服器執行個體的金鑰之後，這個報表伺服器執行個體就無法存取資料庫中的加密資料，此時便從這項向外延展部署中將它有效地移除。  
  
 您必須指定安裝識別碼，才能從向外延展部署中移除報表伺服器執行個體。 安裝識別碼是在您想要移除加密金鑰之報表伺服器執行個體的 RSReportserver.config 檔中儲存的 GUID。 您必須在要從向外延展部署中移除的電腦上執行下列命令。 如果報表伺服器安裝成具名執行個體，請利用 **-i** 引數來指定執行個體。 如需詳細資訊，請參閱 [RsReportServer.config 組態檔](../../reporting-services/report-server/rsreportserver-config-configuration-file.md)。  
  
```  
rskeymgmt -r <installationID>  
```  
  
## <a name="file-location"></a>檔案位置  
 Rskeymgmt.exe 位於 **\<*磁碟機*>:\Program Files\Microsoft SQL Server\110\Tools\Binn** 或 **\<*磁碟機*>:\Program Files (x86)\Microsoft SQL Server\110\Tools\Binn**。 您可以從檔案系統上的任何資料夾執行此公用程式。  
  
## <a name="remarks"></a>Remarks  
 報表伺服器會加密預存的認證和連接資訊。 資料的加密使用公開金鑰和對稱金鑰。 報表伺服器資料庫必須具備有效的金鑰，報表伺服器才能夠執行。 您可以使用 **rskeymgmt** 來備份、刪除或還原金鑰。 如果金鑰無法還原，這個工具可用來刪除已無法使用的加密內容。  
  
 **rskeymgmt** 公用程式用來管理安裝期間或初始化期間所定義的金鑰組。 它利用遠端程序呼叫 (RPC) 端點來連接本機報表伺服器 Windows 服務。 報表伺服器 Windows 服務必須在執行中，這個公用程式才能運作。  
  
 如需加密金鑰的詳細資訊，請參閱[設定和管理加密金鑰 &#40;SSRS 設定管理員&#41;](../../reporting-services/install-windows/ssrs-encryption-keys-manage-encryption-keys.md) 和[初始化報表伺服器 &#40;SSRS 設定管理員&#41;](../../reporting-services/install-windows/ssrs-encryption-keys-initialize-a-report-server.md)。  
  
## <a name="see-also"></a>另請參閱  
 [向外延展部署 - Reporting Services 原生模式 &#40;組態管理員&#41;](http://msdn.microsoft.com/library/4df38294-6f9d-4b40-9f03-1f01c1f0700c)   
 [Reporting Services 報表伺服器 &#40;原生模式&#41;](../../reporting-services/report-server/reporting-services-report-server-native-mode.md)   
 [報表伺服器命令提示字元公用程式 &#40;SSRS&#41;](../../reporting-services/tools/report-server-command-prompt-utilities-ssrs.md)   
 [設定和管理加密金鑰 &#40;SSRS 組態管理員&#41;](../../reporting-services/install-windows/ssrs-encryption-keys-manage-encryption-keys.md)  
  
  
