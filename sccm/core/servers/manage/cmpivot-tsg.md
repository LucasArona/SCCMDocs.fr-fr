---
title: Résoudre les problèmes de CMPivot
titleSuffix: Configuration Manager
description: Découvrez comment résoudre les problèmes liés à CMPivot dans Configuration Manager.
ms.date: 04/04/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 36385bea-f05e-4300-947f-cb3927b3bac5
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: ac95cf355c2b3b97d479f5e3557c1ba74e89977f
ms.sourcegitcommit: 6f4c2987debfba5d02ee67f6b461c1a988a3e201
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/18/2019
ms.locfileid: "59802697"
---
# <a name="troubleshooting-cmpivot"></a>Résoudre les problèmes de CMPivot

CMPivot est un utilitaire de console qui permet d’accéder à l’état en temps réel des appareils de votre environnement. Il exécute immédiatement une requête sur tous les appareils actuellement connectés du regroupement cible, et retourne les résultats. Vous pourrez parfois être amené à devoir résoudre les problèmes liés à CMPivot. Par exemple, vous pouvez constater qu’un client a envoyé un message d’état concernant CMPivot. Toutefois, le serveur de site n’a pas traité le message car il a été endommagé. Cet article vous aide à comprendre le flux des informations concernant CMPivot.

## <a name="get-information-from-the-site-server"></a>Obtenir des informations du serveur de site

Par défaut, le fichiers journaux du serveur de site se trouvent dans C:\Program Files\Microsoft Configuration Manager\logs. Cet emplacement peut varier en fonction de ce qui a été spécifié pour votre répertoire d’installation ou si vous avez déchargé des éléments comme le fournisseur SMS sur un autre serveur.

Cliquez sur le fichier **smsprov.log** pour cette ligne :

```
Auditing: User <username> initiated client operation 135 to collection <CollectionId>.
```

Recherchez l’ID dans la fenêtre CMPivot. Cet ID est la valeur **ClientOperationID**.

![Fenêtre CMPivot avec ClientOperationID en surbrillance](media/cmpivot-clientoperationid.png)

Recherchez la valeur **TaskID** dans la table ClientAction. La valeur **TaskID** correspond à la valeur **UniqueID** dans la table ClientAction. 

```SQL
select * from ClientAction where ClientOperationId=<id>
```

Dans le fichier **BgbServer.log**, recherchez la valeur **TaskID** que vous avez collectée auprès de SQL. Dans le fichier Bgbserver.log, elles est étiquetée **TaskGUID**. Par exemple : 


   - Starting to send push task (PushID: 260 TaskID: 258 TaskGUID: **F8C7C37F-B42B-4C0A-B050-2BB44DF1098A** TaskType: 15 TaskParam:   PFNjcmlwdEhhc2ggU2NyaXB0SGFzaEFsZz0nU0hBMjU2Jz42YzZmNDY0OGYzZjU3M2MyNTQyNWZiNT g2ZDVjYTIwNzRjNmViZmQ1NTg5MDZlMWI5NDRmYTEzNmFiMDE0ZGNjPC9TY3JpcHRIYXNoPjxTY3Jp cHRQYXJhbWV0ZXJzPjxTY3JpcHRQYXJhbWV0ZXIgUGFyYW1ldGVyR3JvdXBHdWlkPSIiIFBhcmFtZX Rlckdyb3VwTmFtZT0iUEdfIiBQYXJhbWV0ZXJOYW1lPSJzZWxlY3QiIFBhcmFtZXRlckRhdGFUeXBlP SJTeXN0ZW0uU3RyaW5nIiBQYXJhbWV0ZXJWaXNpYmlsaXR5PSIwIiBQYXJhbWV0ZXJUeXBlPSIwIiBQ YXJhbWV0ZXJWYWx1ZT0iRGV2aWNlI2tEZXZpY2UjY05hbWUja1N0cmluZyNjTWFudWZhY3R1cmVyI2tTd HJpbmcjY1ZlcnNpb24ja1N0cmluZyNjUmVsZWFzZURhdGUja1N0cmluZyNjU2VyaWFsTnVtYmVyI2tTdH JpbmcjY0J1aWxkTnVtYmVyI2tTdHJpbmcjY1NNQklPU0JJT1NWZXJzaW9uI2tTdHJpbmciLz48U2NyaXB0 UGFyYW1ldGVyIFBhcmFtZXRlckdyb3VwR3VpZD0iIiBQYXJhbWV0ZXJHcm91cE5hbWU9IlBHXyIgUGFyYW 1ldGVyTmFtZT0id21pcXVlcnkiIFBhcmFtZXRlckRhdGFUeXBlPSJTeXN0ZW0uU3RyaW5nIiBQYXJhbWV0ZX JWaXNpYmlsaXR5PSIwIiBQYXJhbWV0ZXJUeXBlPSIwIiBQYXJhbWV0ZXJWYWx1ZT0iU0VMRUNUI3NOYW1lI2N NYW51ZmFjdHVyZXIjY1ZlcnNpb24jY1JlbGVhc2VEYXRlI2NTZXJpYWxOdW1iZXIjY0J1aWxkTnVtYmVyI2 NTTUJJT1NCSU9TVmVyc2lvbiNzRlJPTSNzV2luMzJfQmlvcyIvPjwvU2NyaXB0UGFyYW1ldGVycz48UGFyYW 1ldGVyR3JvdXBIYXNoIFBhcmFtZXRlckhhc2hBbGc9J1NIQTI1NicOTE5NmEwNzNlOTljY2U4MzEyMWE3ZmFi ODE5N2M4M2QxMjhjNDRmNTdlMWI0NGU1NWQwNmU4YTA5NGI5ZGRkNTwvUGFyYW1ldGVyR3JvdXBIYXNoPjwvU 2NyaXB0Q29udGVudD4=-) to 5 clients with throttling (strategy: 1 param: 42) Finished sending push task (PushID: 260 TaskID: 258) to 5 clients

## <a name="client-logs"></a>Journaux du client

Une fois que vous avez les informations du serveur de site, vérifiez les journaux du client. Par défaut, les journaux du client se trouvent dans C:\Windows\CCM\Logs.

Consultez le **CcmNotificationAgent.log**. Vous trouverez des journaux semblables à l’entrée suivante :  

   - **Error! Bookmark not defined.**+PFNjcmlwdEhhc2ggU2NyaXB0SGFzaEFsZz0nU0hBMjU2Jz42YzZmNDY0OGYzZjU3M2MyNTQyNWZiNT g2ZDVjYTIwNzRjNmViZmQ1NTg5MDZlMWI5NDRmYTEzNmFiMDE0ZGNjPC9TY3JpcHRIYXNoPjxTY3Jp cHRQYXJhbWV0ZXJzPjxTY3JpcHRQYXJhbWV0ZXIgUGFyYW1ldGVyR3JvdXBHdWlkPSIiIFBhcmFtZX Rlckdyb3VwTmFtZT0iUEdfIiBQYXJhbWV0ZXJOYW1lPSJzZWxlY3QiIFBhcmFtZXRlckRhdGFUeXBlP SJTeXN0ZW0uU3RyaW5nIiBQYXJhbWV0ZXJWaXNpYmlsaXR5PSIwIiBQYXJhbWV0ZXJUeXBlPSIwIiBQ YXJhbWV0ZXJWYWx1ZT0iRGV2aWNlI2tEZXZpY2UjY05hbWUja1N0cmluZyNjTWFudWZhY3R1cmVyI2tTd HJpbmcjY1ZlcnNpb24ja1N0cmluZyNjUmVsZWFzZURhdGUja1N0cmluZyNjU2VyaWFsTnVtYmVyI2tTdH JpbmcjY0J1aWxkTnVtYmVyI2tTdHJpbmcjY1NNQklPU0JJT1NWZXJzaW9uI2tTdHJpbmciLz48U2NyaXB0 UGFyYW1ldGVyIFBhcmFtZXRlckdyb3VwR3VpZD0iIiBQYXJhbWV0ZXJHcm91cE5hbWU9IlBHXyIgUGFyYW 1ldGVyTmFtZT0id21pcXVlcnkiIFBhcmFtZXRlckRhdGFUeXBlPSJTeXN0ZW0uU3RyaW5nIiBQYXJhbWV0ZX JWaXNpYmlsaXR5PSIwIiBQYXJhbWV0ZXJUeXBlPSIwIiBQYXJhbWV0ZXJWYWx1ZT0iU0VMRUNUI3NOYW1lI2N NYW51ZmFjdHVyZXIjY1ZlcnNpb24jY1JlbGVhc2VEYXRlI2NTZXJpYWxOdW1iZXIjY0J1aWxkTnVtYmVyI2 NTTUJJT1NCSU9TVmVyc2lvbiNzRlJPTSNzV2luMzJfQmlvcyIvPjwvU2NyaXB0UGFyYW1ldGVycz48UGFyYW 1ldGVyR3JvdXBIYXNoIFBhcmFtZXRlckhhc2hBbGc9J1NIQTI1NicOTE5NmEwNzNlOTljY2U4MzEyMWE3ZmFi ODE5N2M4M2QxMjhjNDRmNTdlMWI0NGU1NWQwNmU4YTA5NGI5ZGRkNTwvUGFyYW1ldGVyR3JvdXBIYXNoPjwvU 2NyaXB0Q29udGVudD4=-

Recherchez la valeur **TaskID** dans **Scripts.log**. Dans l’exemple suivant, nous voyons **Task ID {F8C7C37F-B42B-4C0A-B050-2BB44DF1098A}**  :

```
Sending script state message: 7DC6B6F1-E7F6-43C1-96E0-E1D16BC25C14 Scripts 7/3/2018 11:44:47 AM 5036 (0x13AC)
State message: Task Id {F8C7C37F-B42B-4C0A-B050-2BB44DF1098A} Scripts 7/3/2018 11:44:47 AM 5036 (0x13AC)
```

Consultez le fichier **StateMessage.log**. Notre exemple de **TaskID** se trouve en bas du message en regard de &lt;Param>. Vous devez voir des lignes semblables à celle présentée ci-dessous :

```xml
StateMessage body: <?xml version="1.0" encoding="UTF-16"?>
<Report><ReportHeader><Identification><Machine><ClientInstalled>1</ClientInstalled><ClientType>1
</ClientType><ClientID>GUID:DBAC52C9-57E6-47D7-A8D6-E0A5A64B57E6</ClientID><ClientVersion>5.00.8670.1000</ClientVersion>
<NetBIOSName>R613924</NetBIOSName><CodePage>437</CodePage>
<SystemDefaultLCID>1033</SystemDefaultLCID><Priority>0</Priority></Machine></Identification>
<ReportDetails><ReportContent>State Message Data</ReportContent><ReportType>Full</ReportType>
<Date>20180703184447.673000+000</Date><Version>1.0</Version><Format>1.0</Format>
</ReportDetails></ReportHeader><ReportBody><StateMessage MessageTime="20180703184447.517000+000"><Topic ID="7DC6B6F1-E7F6-43C1-96E0-E1D16BC25C14" Type="9003" IDType="0" User="" UserSID=""/><State ID="1" Criticality="0"/>
<StateDetails Type="1"><![CDATA["PAA/AHgAbQBsACAAdgBlAHIAcwBpAG8AbgA9ACIAMQAuADAAIgAgAGUAbgBjAG8AZABpAG4AZwA9ACIAdQB0AGYALQAxADYAIgA/AD4APAByAGUAcwB1AGwAdAAgAFIAZQBzAHUAbAB0AEMAbwBkAGUAPQAiADAAIgA+ADwAZQAgAE4AYQBtAGUAPQAiAEkAbgB0AGUAbAAoAFIAKQAgAFgAZQBvAG4AKABSACkAIABDAFAAVQAgAEUANQAtADIANgA3ADMAIAB2ADQAIABAACAAMgAuADMAMABHAEgAegAiACAATQBhAG4AdQBmAGEAYwB0AHUAcgBlAHIAPQAiAEEAbQBlAHIAaQBjAGEAbgAgAE0AZQBnAGEAdAByAGUAbgBkAHMAIABJAG4AYwAuACIAIABWAGUAcgBzAGkAbwBuAD0AIgBWAFIAVABVAEEATAAgAC0AIAA2ADAAMAAxADcAMAAyACIAIABSAGUAbABlAGEAcwBlAEQAYQB0AGUAPQAiADIAMAAxADcALQAwADYALQAwADIAIAAwADAAOgAwADAAOgAwADAAIgAgAFMAZQByAGkAYQBsAE4AdQBtAGIAZQByAD0AIgAwADAAMAAwAC0AMAAwADEAOAAtADMANgA4ADIALQA0ADcAMAA4AC0ANwA2ADQAMAAtADcANgAwADAALQAzADMAIgAgAFMATQBCAEkATwBTAEIASQBPAFMAVgBlAHIAcwBpAG8AbgA9ACIAMAA5ADAAMAAwADcAIAAiACAALwA+ADwALwByAGUAcwB1AGwAdAA+AA=="~~]]></StateDetails><UserParameters Flags="0" Count="2">
<Param>{F8C7C37F-B42B-4C0A-B050-2BB44DF1098A}</Param><Param>0</Param></UserParameters></StateMessage></ReportBody></Report>
StateMessage 7/3/2018 11:44:47 AM 5036 (0x13AC)
Successfully forwarded State Messages to the MP StateMessage 7/3/2018 11:44:47 AM 5036 (0x13AC)
```

## <a name="review-messages-on-the-site-server"></a>Examiner les messages sur le serveur de site

Ouvrez le fichier **statesys.log** pour voir si le message est reçu et traité. Notre exemple de **TaskID** se trouve en bas du message en regard de &lt;Param>.

```xml
CMessageProcessor - the cmdline to DB exec dbo.spProcessStateReport N'?<?xml version="1.0" encoding="UTF-
16"?>~~<Report><ReportHeader><Identification><Machine><ClientInstalled>1</ClientInstalled><ClientType>1
</ClientType><ClientID>GUID:DBAC52C9-57E6-47D7-A8D6-E0A5A64B57E6</ClientID><ClientVersion>5.00.8670.1000</ClientVersion>
<NetBIOSName>R613924</NetBIOSName><CodePage>437</CodePage>
<SystemDefaultLCID>1033</SystemDefaultLCID><Priority>0</Priority></Machine></Identification>
<ReportDetails><ReportContent>State Message Data</ReportContent><ReportType>Full</ReportType>
<Date>20180703184447.673000+000</Date><Version>1.0</Version><Format>1.0</Format>
</ReportDetails></ReportHeader><ReportBody><StateMessage MessageTime="20180703184447.517000+000"><Topic ID="7DC6B6F1-E7F6-43C1-96E0-E1D16BC25C14" Type="9003" IDType="0" User="" UserSID=""/><State ID="1" Criticality="0"/>
<StateDetails Type="1"><![CDATA["PAA/AHgAbQBsACAAdgBlAHIAcwBpAG8AbgA9ACIAMQAuADAAIgAgAGUAbgBjAG8AZABpAG4AZwA9ACIAdQB0AGYALQAxADYAIgA/AD4APAByAGUAcwB1AGwAdAAgAFIAZQBzAHUAbAB0AEMAbwBkAGUAPQAiADAAIgA+ADwAZQAgAE4AYQBtAGUAPQAiAEkAbgB0AGUAbAAoAFIAKQAgAFgAZQBvAG4AKABSACkAIABDAFAAVQAgAEUANQAtADIANgA3ADMAIAB2ADQAIABAACAAMgAuADMAMABHAEgAegAiACAATQBhAG4AdQBmAGEAYwB0AHUAcgBlAHIAPQAiAEEAbQBlAHIAaQBjAGEAbgAgAE0AZQBnAGEAdAByAGUAbgBkAHMAIABJAG4AYwAuACIAIABWAGUAcgBzAGkAbwBuAD0AIgBWAFIAVABVAEEATAAgAC0AIAA2ADAAMAAxADcAMAAyACIAIABSAGUAbABlAGEAcwBlAEQAYQB0AGUAPQAiADIAMAAxADcALQAwADYALQAwADIAIAAwADAAOgAwADAAOgAwADAAIgAgAFMAZQByAGkAYQBsAE4AdQBtAGIAZQByAD0AIgAwADAAMAAwAC0AMAAwADEAOAAtADMANgA4ADIALQA0ADcAMAA4AC0ANwA2ADQAMAAtADcANgAwADAALQAzADMAIgAgAFMATQBCAEkATwBTAEIASQBPAFMAVgBlAHIAcwBpAG8AbgA9ACIAMAA5ADAAMAAwADcAIAAiACAALwA+ADwALwByAGUAcwB1AGwAdAA+AA=="~~]]></StateDetails><UserParameters Flags="0" Count="2">
<Param>{F8C7C37F-B42B-4C0A-B050-2BB44DF1098A}</Param><Param>0</Param></UserParameters></StateMessage></ReportBody></Report>~~'
```

Vérifiez la boîte de réception des messages d’état si vous ne voyez que le message a été traité. L’emplacement par défaut de cette boîte de réception est C:\Program Files\Microsoft Configuration Manager\inboxes\auth\statesys.box\. Les fichiers se trouvent dans l’un des emplacements suivants :
  
- Entrant
- Endommagé
- Processus

Vérifiez l’affichage de supervision pour CMPivot à partir de SQL à l’aide de la valeur **TaskID**.

```SQL
select * from vSMS_CMPivotStatus where TaskID='{F8C7C37F-B42B-4C0A-B050-2BB44DF1098A}'
```

## <a name="next-steps"></a>Étapes suivantes

[Utilisation de CMPivot](/sccm/core/servers/manage/cmpivot)

[Créer et exécuter des scripts PowerShell](/sccm/apps/deploy-use/create-deploy-scripts)
