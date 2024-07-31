---
title: Broker System Messages
description: "Service Broker uses three system message types to communicate status and error information from Service Broker."
author: rwestMSFT
ms.author: randolphwest
ms.reviewer: mikeray, maghan
ms.date: "03/30/2022"
ms.service: sql
ms.subservice: configuration
ms.topic: reference
---

# Broker System Messages

[!INCLUDE [sql-asdbmi](../../includes/applies-to-version/sql-asdbmi.md)]

Service Broker uses three system message types to communicate status and error information from Service Broker.

## Handling System Messages

Most of the messages in a Service Broker conversation are the application-defined messages used to communicate between services. Each message must comply with a message type format that was defined by a CREATE MESSAGE TYPE statement. The set of message types allowed for a conversation is defined by the contract specified in the BEGIN DIALOG CONVERSATION statement.

In addition to the application-defined message types specified in the contract, any conversation can also receive messages that use one of three system-defined message types. These message types are used by Service Broker to report errors and the status of dialogs. Every application must contain logic to handle Error messages and End Dialog messages. If the application sets a conversation timer on a dialog conversation, the application must contain logic to handle Dialog Timer messages. Service Broker provides these message types to every service, whether they appear in the contract for the service or not. For more information, see [Handling Service Broker Error Messages](handling-service-broker-error-messages.md).

## Error Messages

When a remote service ends a dialog with an error or the local broker detects an unrecoverable error in a dialog, the local broker creates an Error Message. Error messages are of message type `https://schemas.microsoft.com/SQL/ServiceBroker/Error`. Error messages are validated as well-formed XML.

The XML document that is contained in an error message uses the namespace `https://schemas.microsoft.com/SQL/ServiceBroker`. The root element of the document has the local name **Error**, and contains an element named **Code** and an element named **Message**. The **Code** element holds an integer value. The **Message** element holds the human-readable text of the message.

For example, an error message generated by a service that processes expense reports might contain the following XML (reformatted for readability):

```xml
<?xml version="1.0"?>
<Error xmlns="http://schemas.microsoft.com/SQL/ServiceBroker">
  <Code>12</Code>
  <Description>
    Unknown cost center "127-1000". Please check the cost center list
    and resubmit the report.
  </Description>
</Error>
```

A receive operation receives an error message before any message for that dialog other than a dialog timer message. This occurs regardless of the order in which the error message arrived on the queue. When a queue has both a dialog timer message and an error message, a receive operation receives the dialog timer message before the error message.

When an error message arrives for a dialog, the broker raises an error if an application tries to send a message on that dialog. However, an application can receive any remaining messages for the dialog, even after it receives an error message.

## End Dialog Messages

When an application ends a dialog without specifying an error, the local broker sends an End Dialog message to the remote broker. End Dialog messages are of message type `https://schemas.microsoft.com/SQL/ServiceBroker/EndDialog`.

End Dialog messages are empty messages. A receive operation receives an End Dialog message in the order in which the message arrived on the queue.

## Dialog Timer Messages

Dialog timer messages indicate that the conversation timer on a dialog has expired. These messages are of message type `https://schemas.microsoft.com/SQL/ServiceBroker/DialogTimer`. A conversation timer is specific to one side of the conversation; Service Broker never sends a dialog timer message to the other side of the conversation.

Dialog timer messages are empty messages. A receive operation receives the dialog timer message before any other message for that dialog, regardless of the order in which the time-out message arrived on the queue.

## See also

- [How to: Retrieve Information from a Service Broker Error Message (Transact SQL)](how-to-retrieve-information-from-a-service-broker-error-message-transact-sql.md)
- [BEGIN CONVERSATION TIMER (Transact-SQL)](../../t-sql/statements/begin-conversation-timer-transact-sql.md)
- [BEGIN DIALOG CONVERSATION (Transact-SQL)](../../t-sql/statements/begin-dialog-conversation-transact-sql.md)
- [CREATE CONTRACT (Transact-SQL)](../../t-sql/statements/create-contract-transact-sql.md)
- [CREATE MESSAGE TYPE (Transact-SQL)](../../t-sql/statements/create-message-type-transact-sql.md)
- [END CONVERSATION (Transact-SQL)](../../t-sql/statements/end-conversation-transact-sql.md)
- [RECEIVE (Transact-SQL)](../../t-sql/statements/receive-transact-sql.md)