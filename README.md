
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
#include <pthread.h>

pthread_t th[3];

void *fonc(void *i)
{
    printf("Je suis le %ld thread identifie par le PID=%d et le numero=%lu\n",
           (long)i + 1, getpid(), (unsigned long)pthread_self());
    return NULL;
}

int main(void)
{
    int i;

    for (i = 0; i < 3; i++)
        pthread_create(&th[i], NULL, fonc, (void *)(long)i);

    for (i = 0; i < 3; i++)
        pthread_join(th[i], NULL);

    printf("Je suis le thread initial PID=%d numero=%lu\n",
           getpid(), (unsigned long)pthread_self());

    return 0;
}
