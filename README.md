# Projeto-MovimentarRatoo

#include <iostream>
#include <windows.h>
using namespace std;

const char ESPACO ='.';
const char PAREDE = 'P';
const char QUEIJO ='Q';
const char ENTRADA ='E';
const char RATO ='R';
const char PEGO ='X';

#define CIMA 0
#define BAIXO 1
#define ESQUERDA 2
#define DIREITA 3
#define INICIO 4

const int LARGURA = 5;
const int ALTURA = 5;

void criarMapa(char mapa[LARGURA][ALTURA]){
    for(int i=0; i<LARGURA; i++){
        for(int j=0; j<ALTURA; j++){
            mapa[i][j] = ESPACO;
        }
    }
}

void exibirMapa(char mapa[LARGURA][ALTURA], int posX, int posY){
    for(int i=0; i<LARGURA; i++){

        for(int j=0; j<ALTURA; j++){
            if (posX == i && posY == j){
                mapa[i][j] = RATO;
                cout << mapa[i][j];
            }
            else if (mapa[i][j] == RATO){
                mapa[i][j] = PEGO;
                cout << mapa[i][j];
            }

            cout << mapa[i][j] << "\t";
        } 


    cout << endl;  
    }
}

bool procurarQueijoNaoImplementado(char mapa[LARGURA][ALTURA],int posX,int posY, int deOndeVeio, bool &temQueijo){
    if(posX < 0 || posY < 0 || posX >= LARGURA || posY >= ALTURA){
        return false;
    }else if(mapa[posX][posY]==QUEIJO){
        temQueijo = true;
        cout << "Voce encontrou o queijo!" << endl;
        exibirMapa(mapa, posX, posY);
        cout << endl;
        Sleep(1500);
        return true;
    }else if(mapa[posX][posY]==PAREDE || mapa[posX][posY] == RATO){
        return false;
    }else{
        exibirMapa(mapa, posX, posY);
        cout << endl;
        Sleep(1500);

        if(deOndeVeio != DIREITA and procurarQueijoNaoImplementado(mapa,posX,posY+1, ESQUERDA, temQueijo)){
            exibirMapa(mapa, posX, posY);
            cout << endl;
            Sleep(1500);
            return true;
        }else if(deOndeVeio != BAIXO and procurarQueijoNaoImplementado(mapa,posX+1,posY, CIMA, temQueijo)){
            exibirMapa(mapa, posX, posY);
            cout << endl;
            Sleep(1500);
            return true;
        }else if(deOndeVeio != ESQUERDA and procurarQueijoNaoImplementado(mapa,posX,posY-1, DIREITA, temQueijo)){
            exibirMapa(mapa, posX, posY);
            cout << endl;
            Sleep(1500);
            return true;
        }else if(deOndeVeio != CIMA and procurarQueijoNaoImplementado(mapa,posX-1,posY, BAIXO, temQueijo)){
           exibirMapa(mapa, posX, posY);
            cout << endl;
            Sleep(1500);
            return true;
        }
    }
    return false;
}

int main(){
    char mapa[LARGURA][ALTURA];
    int posX = 0, posY = 0;
    int deOndeVeio;
    bool temQueijo = false;
    criarMapa(mapa);
    
    mapa[0][0] = ENTRADA;
    mapa[1][1] = PAREDE;
    mapa[2][2] = PAREDE;
    mapa[2][3] = PAREDE;
    mapa[3][2] = PAREDE;
    mapa[3][3] = QUEIJO;

    procurarQueijoNaoImplementado(mapa, posX, posY, deOndeVeio, temQueijo);
    exibirMapa(mapa, posX, posY);
   
    return 0;
}
