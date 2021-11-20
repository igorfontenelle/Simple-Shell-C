#include <stdio.h>
#include <unistd.h>
#include <sys/types.h>
#include <sys/wait.h>
#include <stdlib.h>
#include <errno.h>
/**
Demontração do uso do shell 
**/
int main(int argc, char *argv[]){
  pid_t pid;
  int status;
  if(!(pid = fork())) {
      //Codigo do filho
      if (argc>4){
		printf("Uso: \n\t\t %s <cmd> <arg1> <arg2>\n\n",argv[0]);
        printf("O comando deve possuir no máximo 2 argumentos");
		exit(1);
	}
      execlp(argv[1],argv[1],argv[2], argv[3], NULL) ;
 
  }
  
  // Execucao pelo pai
  waitpid(pid,&status,WUNTRACED);
  if(WIFEXITED(status)) { 
      printf("\nSaída Normal\n");
      printf("Exit status: %d\n",WEXITSTATUS(status)); 
  }else{ 
      printf("Saída NÃO Normal - erro\n"); 
  } 
  return 0;
}