# Nachos


# Project 1: Threads

#### Miembros del grupo
- Lluque Delgado Paul
- Mejía Tasayco Juan Jose
- Urbina Quispe Jaime Gerardo
- Torres Cerron Vladimir
- Anccasi Huiza Edda Juliet

---------------------------------------------------------------------------------

###Locks And Conditions

Nosotros implementamos, adquirimos y lanzamos usando interrupciones, 
afirmaciones, esperar y cola de preparados. Del mismo modo, las variables 
de condición utilizan interrupciones, espera y listo colas y cerraduras. 
En lugar de añadir a la cola de espera, utilizamos SortedInsert() to prioritize 
the threads.

    Test switch case numbers used:
        2: Expects to work successfully
        3: Assert should fail: Cannot delete a held lock by own thread
        4: Assert should fail: Cannot delete a held lock by another thread
        5: Assert Should fail: Cannot wait without holding a lock
        6: Expects to work successfully
        7: Expects to work successfully
        8: Assert fails: Cannot delete while threads on queue
---------------

###Mailbox

Utilizamos cerraduras, y variables de condición canSend y canReceive así como una
bool nombre completo . nos aseguramos de entrelazado por inversión de llamar a la condición
variables envían y reciben . aficionado a la variable contiene la palabra , y el pleno
asegura que sólo un remitente interactúa con un receptor.


    Los números utilizados en los casos de prueba son:
        9: Expects to work succesfully as sender comes first
        10:Expects to work succesffully as receiver comes first
        11:Only sender is available. Synchronization can not be achieved.
        12:Only receiver is available. Synchronization can not be achieved.
        13:Expects to work. Interleaving between senders and receivers
---------------

###Join
Agregamos varias variables miembro de la clase Thread , incluyendo booleanos
que indican si el mensaje ha bifurcado ( hasForked ) , si el hilo es
acoplable ( willBeJoined - juego basado en argumento del constructor ) , y si el hilo
ya se ha unido ( hasJoined ) , así como una cerradura y una variable de estado.
Cuando un padre invoca Join ( ) en un hijo , el hijo adquiere el bloqueo y pone al
padre para dormir hasta que el hilo hijo haya terminado .
Una vez que termina una rosca , a través de una llamada a Finalizar (), se comprueba su estado de hasJoined y willBeJoined .
Si se va a unir , pero no tiene; sin embargo, se va a esperar para ensamblar el que se invoca y regresó .
Después, se fijará como listos para ser destruidos .

    Los números utilizados en los casos de prueba son:
        21: a thread that will be joined only is destroyed once Join has been called on it
        22: if a parent calls Join on a child and the child is still executing, the parent waits
        23: if a parent calls Join on a child and the child has finished executing, the parent does not block
        24: a thread does not call join on itself 
        25: join is only invoked on threads created to be joined
        26: join is only called on a thread that has forked
        27: join is not called more than once on a thread
----------

###Priorities

Se trabajó sobre las prioridades mediante la utilización de la función SortedInsert ( ) en la lista. 
Sin embargo, esta función ordena originalmente por orden ascendente . Queremos que el orden sea descendente.
Para ello, basta con pasar una negación de la prioridad a la función de lograr los resultados esperados. 
Luego se modificó Tema :: Rendimiento () de modo que el hilo de alta prioridad va a volver a sí mismo
si no hay otro hilo tiene mayor prioridad .

    Los números utilizados en los casos de prueba son:
       19: Expects to work successfully. Outputs for all test cases will be display on 
the screen after running "./nachos -q 19".

Those test cases include:

       <1> Priority test for scheduler. When Thread::Yield() is called, the scheduler 
              always run the thread with the highest priority, or switch between threads that share 
              the highest priority.
       <2> Priority test for synch primiives Lock.
       <3> Priority test for Semaphore.
       <4> Priority test for Condition Var, waked up by Signal();
       <5> Priority test for Condition Var, waked up by Broadcast();
       <6> [Extra Credit] There are 5 threads in this case. The lock-holding thread is successfully promoted, 
              so that it exits before all mid-priority threads finish. 
       <7> [Extra Credit] There are 4 threads in this case. The joinee is successfully promoted, so that it 
              exits before all mid-priority threads finish.
       <8> [Extra Credit] There are 6 threads in this case. When Join() is called, the joinee (it is also the lock 
              waiter) is promoted, as well as the lock holder. So that they exit before all mid-priority threads.

------------

###Whales
We used 4 semaphores to implement whale matching. There are 3 functions with similar codes male, female and matchmaker representing whales from each class. There are four semaphores thus four wait lists, one for each whale class to make sure only one whale from each class is waiting to be matched, and another for whales to wait for being matched. Only when 3 whales from each of the 3 classes come, can they form a match and then return, otherwise wait. To make things clear, we add variables to indicate the number of match and whales from each classes, when a male whale comes or returns, the program will print "one male whale come(return from match NO.#)" and then print out the number of male whales waiting to be matched, when female and matchmaker come or return, the program will print similar message. And when a match 
completed it will print "match NO.# completed"

    Test switch case numbers used:
         30: 9 whales in 3 pairs, 3 male, 3 female, 3 matchmaker, three matches succeed
         31: 8 whales , 3 male, 3 female, 2 matchmaker, only two matches succeed
         32: 7 whales , 3 male, 1 female, 3 matchmaker, only one match succeeds
         33: 9 whales in 3 pairs, 3 male, 3 female, 3 matchmaker, in a different order, three matches succeed
         
	 we also tried -rs while testing and our program works fine in random switch circumstance
         use -d w and -d x to see debug information

-------------------
