# Message3-Include

This include was created to help people keep their chat box on the server clean and only for chat. i have made all other messages that are not to do with players chatting to other players into textdraws so the chat is only for chat purposes, with the include you can send Usage, Error, Info, Adverts and Admin messages. Everyone has there own way they play so i added so each player can position their own messages to their own desire.

At the top of your code use include <message3>

Features:
Creates an indiviual textdraw for cetian messages
prevents chat spam of unwanted messages

Requirements:
zcmd.inc // include this into your gamemode before the Message2.inc (without this the include will not function).
sscanf2.inc // include this into your gamemode before the Message2.inc (without this the include will not function).
foreach.inc // include this into your gamemode before the Message2.inc (without this the include will not function).
sscanf.dll/.so // Dont forget to put this in your plugin folder and write on the line "plugins" on your server.cfg.

Message Styles:
Code:
MSG_STYLE_ERROR    1
MSG_STYLE_INFO     2
MSG_STYLE_USAGE    3
MSG_STYLE_ADVERT   4
MSG_STYLE_ADMIN    5

Functions:

SendServerMessage(playerid, msgstyle, const message[]);
CreateMessageTextDraw(playerid); // Place under OnPlayerConnect(playerid) Otherwise the textdraws will not show
DestroyMessageTextDraw(playerid); // Place Under OnPlayerDisconnect(playerid, reason) Otherwise the textdraws will not show

Commands:
/msgpos - Usage /msgpos [Custom X] [Custom Y].
/defaultmsg

Example Codes:

CMD:goto(playerid, params[])
{
    new pID,Float:Pos[3], string[50];
    if(pInfo[playerid][Adminlvl] < 3) return SendServerMessage(playerid, MSG_STYLE_ERROR ,"You are not high enough admin level!");  // New Code!!
    if(sscanf(params, "u", pID)) return SendServerMessage(playerid, MSG_STYLE_USAGE,"Usage: /goto [ID]");  // New 	Code!!
    if(pID == IPI) return SendServerMessage(playerid, MSG_STYLE_ERROR,"Player is not connected!"); // New Code!!
    GetPlayerPos(pID,Pos[0],Pos[1],Pos[2]);
    SetPlayerPos(playerid,Pos[0],Pos[1],Pos[2]); 
    SetPlayerInterior(playerid,GetPlayerInterior(pID));
    format(string,sizeof(string),"Admin %s has teleported to you",GetName(playerid));
    SendServerMessage(playerid, MSG_STYLE_INFO, str);  // New Code!!
    return 1;
}

CMD:atalk(playerid, params[])
{
	new text[128];
	if(sscanf(params, "s[128]", text)) return SendServerMessage(playerid, MSG_STYLE_USAGE, "/atalk [text]");
	SendServerMessage(playerid, MSG_STYLE_ADMIN, text);
	return 1;
}
