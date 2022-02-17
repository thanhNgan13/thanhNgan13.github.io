# thanhNgan13.github.io
void gotoxy(short x, short y) {

COORD pos = { x, y };

SetConsoleCursorPosition(GetStdHandle(STD_OUTPUT_HANDLE), pos);

}

-------------------------------------------------------

void set_color ( int code ) {

HANDLE color = GetStdHandle(STD_OUTPUT_HANDLE);

SetConsoleTextAttribute( color , code );

}

set_color( X )
