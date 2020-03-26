## SMTP 状态码
状态码 |Description|描述
---|---|---
211 | System status, or system help reply|系统状态或显示系统帮助。
214|Help message|显示系统帮助，通常用于显示非标准命令的帮助。
220|Service ready|服务就绪。
221|Service closing transmission channel|服务关闭了传输通道。
250|Requested mail action okay, completed|所要求的邮件动作完成，可以继续邮件对话。通常在EHLO/HELO命令后会通过“250-”来描述服务器所支持的特性。
251|User not local; will forward to|收件人非本地用户，将转发到 。
354|Start mail input; end with .|开始接收邮件内容输入，以.(即单行一个点)结束输入。
421|Service not available, closing transmission channel|无法提供正常服务，关闭传输管道。邮件保留在本地，可能会尝试重新投递。通常这种情况发生在服务器遇到问题，必须关闭传输。
450|Requested mail action not taken: mailbox unavailable|所要求的邮件动作无法执行：邮箱不可用。邮件保留在本地，可能会尝试重新投递。通常这种情况发生在邮箱忙或被拒绝等。
451|Requested action aborted: local error in processing|要求动作中断：本地端发生错误。邮件保留在本地，可能会尝试重新投递。通常这种情况发生在系统投递时遇到意外的错误。
452|Requested action not taken: insufficient system storage |要求动作无法执行：系统空间不足。邮件保留在本地，可能会尝试重新投递。通常这种情况发生在邮箱限额满。
500| Syntax error, command unrecognized|命令格式错误，不可识别。当命令行太长时也会发生这样的错误。
501|Syntax error in parameters or arguments|命令参数错误。
502|Command not implemented|命令尚未实现。
503|Bad sequence of commands|错误的命令顺序。
504|Command parameter not implemented|命令的参数尚未实现。
550|Requested action not taken: mailbox unavailable|所要求动作无法执行：信箱不存在。不再尝试投递。
551|User not local; please try|收件人不属于本地用户，转发到。不再尝试投递。
552|Requested mail action aborted: exceeded storage allocation|所要求的动作中断：超出所分配的储存空间。不再尝试投递。
553|Requested action not taken: mailbox name not allowed|所要求的动作未执行：不接受该信箱。通常发生在邮件地址错误、被作为垃圾邮件拒收。不再尝试投递。
554|Transaction failed传输失败。
