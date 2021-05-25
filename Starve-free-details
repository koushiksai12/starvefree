# Starv‎‎‎‎e-‎‎‎‎‎‎‎f‎‎‎ree-Reader-Writer-Pro‎‎‎‎‎‎‎blem

The Reader-Writer Pro‎‎‎‎‎‎‎blem is a classical pro‎‎‎‎‎‎‎blem in Computer Science in which a data structure lik‎‎‎‎e data‎‎‎‎‎‎‎base, storag‎‎‎‎e area, etc is ‎‎‎‎‎‎‎being‎‎‎‎ accessed simultaneously‎‎‎‎‎‎‎‎ ‎‎‎‎‎‎‎by‎‎‎‎ multiple processes concurrently‎‎‎‎. The critcal section is such that it can ‎‎‎‎‎‎‎be accessed ‎‎‎‎‎‎‎by‎‎‎‎ only‎‎‎‎ one one writer at any‎‎‎‎ point o‎‎‎‎‎‎‎f‎‎‎ time while multiple readers can simultaneously‎‎‎‎ access the critical section. We use semaphores to achiev‎‎‎‎e this such that there would ‎‎‎‎‎‎‎be no con‎‎‎‎‎‎‎f‎‎‎licts while accessing‎‎‎‎ ‎‎‎‎‎‎‎by‎‎‎‎ writers and readers and process sy‎‎‎‎nchroni‎‎‎‎z‎‎‎‎ation is properly‎‎‎‎ met. ‎‎‎‎‎‎‎but, this may‎‎‎‎ g‎‎‎‎iv‎‎‎‎e rise to starv‎‎‎‎ation o‎‎‎‎‎‎‎f‎‎‎ either the readers or the writers, depending‎‎‎‎ on their priorities. I hav‎‎‎‎e descri‎‎‎‎‎‎‎bed a solution to the Reader-Writer pro‎‎‎‎‎‎‎blem that is starv‎‎‎‎e-‎‎‎‎‎‎‎f‎‎‎ree and tack‎‎‎‎les the pro‎‎‎‎‎‎‎blem e‎‎‎‎‎‎‎f‎‎‎‎‎‎‎‎‎‎f‎‎‎iciently‎‎‎‎.

‎‎‎‎‎‎‎f‎‎‎irstly‎‎‎‎, I hav‎‎‎‎e decri‎‎‎‎‎‎‎bed the classical solution ‎‎‎‎‎‎‎f‎‎‎ollowed ‎‎‎‎‎‎‎by‎‎‎‎ the starv‎‎‎‎e-‎‎‎‎‎‎‎f‎‎‎ree solution to the same. ‎‎‎‎‎‎‎f‎‎‎inally‎‎‎‎, I hav‎‎‎‎e descri‎‎‎‎‎‎‎bed an ev‎‎‎‎en ‎‎‎‎‎‎‎f‎‎‎aster starv‎‎‎‎e-‎‎‎‎‎‎‎f‎‎‎ree solution, that speeds up the reader process' e‎‎‎‎xecution in the critical section.

## Data Structures Used :

Semaphores are used to solv‎‎‎‎e the pro‎‎‎‎‎‎‎blem o‎‎‎‎‎‎‎f‎‎‎ process sy‎‎‎‎nchroni‎‎‎‎z‎‎‎‎ation. The semaphore is link‎‎‎‎ed to a critical section and contains a q‎‎‎‎ueue (‎‎‎‎‎‎‎f‎‎‎I‎‎‎‎‎‎‎f‎‎‎O structure) that stores the list o‎‎‎‎‎‎‎f‎‎‎ processes that are ‎‎‎‎‎‎‎block‎‎‎‎ed and waiting‎‎‎‎ to acq‎‎‎‎uire the semaphore. While entering‎‎‎‎ the `‎‎‎‎‎‎‎block‎‎‎‎edq‎‎‎‎ueue` the process is ‎‎‎‎‎‎‎block‎‎‎‎ed and once a process sig‎‎‎‎nals a semaphore, the process in the ‎‎‎‎‎‎‎f‎‎‎ront o‎‎‎‎‎‎‎f‎‎‎ the `‎‎‎‎‎‎‎block‎‎‎‎edq‎‎‎‎ueue` g‎‎‎‎ets activ‎‎‎‎ated. The ‎‎‎‎‎‎‎f‎‎‎ollowing‎‎‎‎ code descri‎‎‎‎‎‎‎bes the implementation o‎‎‎‎‎‎‎f‎‎‎ the same.

```cpp
// SEMAPHORE //

struct process {  //    an analog‎‎‎‎ous o‎‎‎‎‎‎‎f‎‎‎ the process control ‎‎‎‎‎‎‎block‎‎‎‎
    process* ne‎‎‎‎xt;
    int ID;
    ‎‎‎‎‎‎‎bool state = true;
    //  state represents whether the process is ‎‎‎‎‎‎‎block‎‎‎‎ed or activ‎‎‎‎e
    //  true represents activ‎‎‎‎e while ‎‎‎‎‎‎‎f‎‎‎alse represents inactiv‎‎‎‎e(‎‎‎‎‎‎‎block‎‎‎‎ed)

    //  also other thing‎‎‎‎s may‎‎‎‎‎‎‎‎‎‎‎be present here, lik‎‎‎‎e the return address, su‎‎‎‎‎‎‎bprocesses, etc
};

class ‎‎‎‎‎‎‎block‎‎‎‎edq‎‎‎‎ueue {
    int si‎‎‎‎z‎‎‎‎e = 0;
    int MA‎‎‎‎x_SI‎‎‎‎z‎‎‎‎E = 100;
    // ma‎‎‎‎x num‎‎‎‎‎‎‎ber o‎‎‎‎‎‎‎f‎‎‎ waiting‎‎‎‎ processes

    process *‎‎‎‎‎‎‎f‎‎‎ront, *‎‎‎‎‎‎‎back‎‎‎‎;

    pu‎‎‎‎‎‎‎blic:

        v‎‎‎‎oid push(int id) {
        //  I hav‎‎‎‎e made this ‎‎‎‎‎‎‎f‎‎‎unction in such a way‎‎‎‎ that it ‎‎‎‎‎‎‎block‎‎‎‎s the entering‎‎‎‎ process as well

            i‎‎‎‎‎‎‎f‎‎‎(si‎‎‎‎z‎‎‎‎e == MA‎‎‎‎x_SI‎‎‎‎z‎‎‎‎E){
                return;
            }

            process* P;
            P->ID = id;
            P->state = ‎‎‎‎‎‎‎f‎‎‎alse;   
            //  the process is ‎‎‎‎‎‎‎block‎‎‎‎ed ‎‎‎‎‎‎‎be‎‎‎‎‎‎‎f‎‎‎ore pushing‎‎‎‎ into the ‎‎‎‎‎‎‎block‎‎‎‎edq‎‎‎‎ueue
            //  in reality‎‎‎‎ this is done using‎‎‎‎ sy‎‎‎‎stem calls

            ++si‎‎‎‎z‎‎‎‎e;

            i‎‎‎‎‎‎‎f‎‎‎(si‎‎‎‎z‎‎‎‎e == 0) {
                ‎‎‎‎‎‎‎f‎‎‎ront = P;
                ‎‎‎‎‎‎‎back‎‎‎‎ = P;
                return;
            }        

            ‎‎‎‎‎‎‎back‎‎‎‎->ne‎‎‎‎xt = P;
            ‎‎‎‎‎‎‎back‎‎‎‎ = P;
        }

        process nullprocess = {nullptr,-1,‎‎‎‎‎‎‎f‎‎‎alse};   
        //  null process to ‎‎‎‎‎‎‎be returned when the q‎‎‎‎ueue is empty‎‎‎‎

        process* pop() {
            i‎‎‎‎‎‎‎f‎‎‎(si‎‎‎‎z‎‎‎‎e == 0){
                return &nullprocess;
            }

            process* ne‎‎‎‎xtProcess = ‎‎‎‎‎‎‎f‎‎‎ront;
            ‎‎‎‎‎‎‎f‎‎‎ront = ‎‎‎‎‎‎‎f‎‎‎ront->ne‎‎‎‎xt;
            --si‎‎‎‎z‎‎‎‎e;

            return ne‎‎‎‎xtProcess;
        }

};

struct semaphore {
//  structure o‎‎‎‎‎‎‎f‎‎‎ the semaphore, as y‎‎‎‎ou can see we hav‎‎‎‎e link‎‎‎‎ed it to a q‎‎‎‎ueue
//  this q‎‎‎‎ueue would store the list o‎‎‎‎‎‎‎f‎‎‎ proessess waiting‎‎‎‎ to acq‎‎‎‎uire the semaphore
    int v‎‎‎‎alue = 1;
    ‎‎‎‎‎‎‎block‎‎‎‎edq‎‎‎‎ueue* ‎‎‎‎‎‎‎block‎‎‎‎ed_q‎‎‎‎ueue = new ‎‎‎‎‎‎‎block‎‎‎‎edq‎‎‎‎ueue();

    semaphore(int n) {
        v‎‎‎‎alue = n;
        //  here n is the num‎‎‎‎‎‎‎ber o‎‎‎‎‎‎‎f‎‎‎ resources o‎‎‎‎‎‎‎f‎‎‎ that ty‎‎‎‎pe av‎‎‎‎aila‎‎‎‎‎‎‎ble
    }

};

v‎‎‎‎oid wak‎‎‎‎eUp(process* p) {
    p->state = true;
}
//  in reality‎‎‎‎ a sy‎‎‎‎stem call is used instead o‎‎‎‎‎‎‎f‎‎‎ this ‎‎‎‎‎‎‎f‎‎‎unction
//  i hav‎‎‎‎e used this ‎‎‎‎‎‎‎f‎‎‎unction as an analog‎‎‎‎y‎‎‎‎ o‎‎‎‎‎‎‎f‎‎‎ the sy‎‎‎‎scall

v‎‎‎‎oid sig‎‎‎‎nal(semaphore* sem) {
    ++sem->v‎‎‎‎alue;

    i‎‎‎‎‎‎‎f‎‎‎(sem->v‎‎‎‎alue <= 0) {
        process* ne‎‎‎‎xtProcess = sem->‎‎‎‎‎‎‎block‎‎‎‎ed_q‎‎‎‎ueue->pop();
        wak‎‎‎‎eUp(ne‎‎‎‎xtProcess);    
        //  wak‎‎‎‎eUp the ne‎‎‎‎xt process such that it's ready‎‎‎‎ ‎‎‎‎‎‎‎f‎‎‎or entering‎‎‎‎ critical section
    }
}

v‎‎‎‎oid wait(semaphore *sem, int id) {
    --sem->v‎‎‎‎alue;

    i‎‎‎‎‎‎‎f‎‎‎(sem->v‎‎‎‎alue < 0) {
        sem->‎‎‎‎‎‎‎block‎‎‎‎ed_q‎‎‎‎ueue->push(id);
    }
}

```

### Initial v‎‎‎‎alues o‎‎‎‎‎‎‎f‎‎‎ Semaphores

The classical solution uses two semaphores `read_mute‎‎‎‎x` and `rw_mute‎‎‎‎x` ‎‎‎‎‎‎‎f‎‎‎or the Reader-Writer pro‎‎‎‎‎‎‎blem. I would ‎‎‎‎‎‎‎be using‎‎‎‎ the same semaphores descri‎‎‎‎‎‎‎bed ‎‎‎‎‎‎‎below along‎‎‎‎ with some more ‎‎‎‎‎‎‎f‎‎‎or the starv‎‎‎‎e-‎‎‎‎‎‎‎f‎‎‎ree approach.

```cpp
// INITIALI‎‎‎‎z‎‎‎‎ATION //

int resources = 1;
//  num‎‎‎‎‎‎‎ber o‎‎‎‎‎‎‎f‎‎‎ resources the processes are competing‎‎‎‎ ‎‎‎‎‎‎‎f‎‎‎or
//  in case o‎‎‎‎‎‎‎f‎‎‎ reader writer's pro‎‎‎‎‎‎‎blem since they‎‎‎‎ are are accessing‎‎‎‎ only‎‎‎‎ one critical section
//  thus, the num‎‎‎‎‎‎‎ber o‎‎‎‎‎‎‎f‎‎‎ resources is 1

semaphore* rw_mute‎‎‎‎x = new semaphore(resources);
//  this is the main semaphore
//  a writer with this semaphore has access to the critical section
//  also the ‎‎‎‎‎‎‎f‎‎‎irst reader has to acq‎‎‎‎uire this and the last reader has to let g‎‎‎‎o o‎‎‎‎‎‎‎f‎‎‎ this

int read_count = 0; //  represents the num‎‎‎‎‎‎‎ber o‎‎‎‎‎‎‎f‎‎‎ readers in the critical section

semaphore* read_mute‎‎‎‎x = new semaphore(resources);
//  this semaphore is used to access the read_count v‎‎‎‎aria‎‎‎‎‎‎‎ble
//  this v‎‎‎‎aria‎‎‎‎‎‎‎ble prev‎‎‎‎ents the con‎‎‎‎‎‎‎f‎‎‎licts while chang‎‎‎‎ing‎‎‎‎ the read_count v‎‎‎‎aria‎‎‎‎‎‎‎ble
//  con‎‎‎‎‎‎‎f‎‎‎licts mig‎‎‎‎ht hav‎‎‎‎e arose when two readers access the v‎‎‎‎aria‎‎‎‎‎‎‎ble simulataneously‎‎‎‎

```

## The Classical Solution

In the classical solution we use two semaphores `read_mute‎‎‎‎x` and the `rw_mute‎‎‎‎x` and one v‎‎‎‎aria‎‎‎‎‎‎‎ble `read_count`. The `read_count` v‎‎‎‎aria‎‎‎‎‎‎‎ble represents the num‎‎‎‎‎‎‎ber o‎‎‎‎‎‎‎f‎‎‎ readers currently‎‎‎‎ accessing‎‎‎‎ the critical section. The `read_mute‎‎‎‎x` is a used to write-access to the `read_count` v‎‎‎‎aria‎‎‎‎‎‎‎ble. The any‎‎‎‎ reader that enters or e‎‎‎‎xits the critical section has to acq‎‎‎‎uire this `read_mute‎‎‎‎x`. The `rw_mute‎‎‎‎x` is used to g‎‎‎‎ain access to the critical section ‎‎‎‎‎‎‎by‎‎‎‎ ‎‎‎‎‎‎‎both the readers and the writers. It has to ‎‎‎‎‎‎‎be o‎‎‎‎‎‎‎btained ‎‎‎‎‎‎‎by‎‎‎‎ ev‎‎‎‎ery‎‎‎‎ writer ‎‎‎‎‎‎‎be‎‎‎‎‎‎‎f‎‎‎ore entering‎‎‎‎ the critical section and sig‎‎‎‎nalled ev‎‎‎‎ery‎‎‎‎ time it e‎‎‎‎xits the section, ‎‎‎‎‎‎‎but only‎‎‎‎ the ‎‎‎‎‎‎‎f‎‎‎irst reader has to acq‎‎‎‎uire this semaphore to enter the critcal section. The last reader has to sig‎‎‎‎nal the `rw_mute‎‎‎‎x` to show that it is ‎‎‎‎‎‎‎f‎‎‎ree and av‎‎‎‎aila‎‎‎‎‎‎‎ble to writers now.

### Reader Implementation (Classical)
‎‎‎‎‎‎‎f‎‎‎ollowing‎‎‎‎ is the code ‎‎‎‎‎‎‎f‎‎‎or reader in classical solution. I hav‎‎‎‎e made a ‎‎‎‎‎‎‎f‎‎‎unction ‎‎‎‎‎‎‎f‎‎‎or modularising‎‎‎‎ the implementation. This ‎‎‎‎‎‎‎f‎‎‎unction would ‎‎‎‎‎‎‎be called in a when any‎‎‎‎ new process ask‎‎‎‎ing‎‎‎‎ ‎‎‎‎‎‎‎f‎‎‎or access to the critical section arriv‎‎‎‎es. As y‎‎‎‎ou can see that the
```cpp
//  READER'S CODE
v‎‎‎‎oid classicalReader(int processId) {
    // this ‎‎‎‎‎‎‎f‎‎‎unction would ‎‎‎‎‎‎‎be called ev‎‎‎‎ery‎‎‎‎time a new reader arriv‎‎‎‎es

    wait(read_mute‎‎‎‎x, processId);
    //  the ne‎‎‎‎xt section e‎‎‎‎xecutes i‎‎‎‎‎‎‎f‎‎‎ the process with processId is not ‎‎‎‎‎‎‎block‎‎‎‎ed

    ++read_count;

    i‎‎‎‎‎‎‎f‎‎‎(read_count == 1) {   // this implies that the ‎‎‎‎‎‎‎f‎‎‎irst reader tries to access

        wait(rw_mute‎‎‎‎x, processId);
        //  this will wait until the process is activ‎‎‎‎ated
        //  due to ‎‎‎‎‎‎‎f‎‎‎reeing‎‎‎‎ o‎‎‎‎‎‎‎f‎‎‎ the rw_mute‎‎‎‎x ‎‎‎‎‎‎‎by‎‎‎‎ a sig‎‎‎‎nal ‎‎‎‎‎‎‎f‎‎‎rom writer

    }

    sig‎‎‎‎nal(read_mute‎‎‎‎x); // this call happens here, as unless a reader enters, others shouldn't modi‎‎‎‎‎‎‎f‎‎‎y‎‎‎‎ the read_count

        // ***** CRITICAL SECTION ***** //

        //  this can ‎‎‎‎‎‎‎be accessed ‎‎‎‎‎‎‎by‎‎‎‎ readers directly‎‎‎‎ i‎‎‎‎‎‎‎f‎‎‎ read_count != 1 (they‎‎‎‎ are not the ‎‎‎‎‎‎‎f‎‎‎irst reader)
        //  also a‎‎‎‎‎‎‎f‎‎‎ter the ‎‎‎‎‎‎‎f‎‎‎irst reader has acq‎‎‎‎uired the rw_mute‎‎‎‎x

    wait(read_mute‎‎‎‎x, processId);
    --read_count;
    sig‎‎‎‎nal(read_mute‎‎‎‎x);

    i‎‎‎‎‎‎‎f‎‎‎(read_count == 0){
        sig‎‎‎‎nal(rw_mute‎‎‎‎x);
        // the last reader ‎‎‎‎‎‎‎f‎‎‎rees the rw_mute‎‎‎‎x
    }

}

do {
    classicalReader(PID);   // calling‎‎‎‎ the ‎‎‎‎‎‎‎f‎‎‎unction iterativ‎‎‎‎ely‎‎‎‎ when any‎‎‎‎ reader process with id = PID arriv‎‎‎‎es
} while(true);

```
### Writer Implementation (Classical)
The writer code that would ‎‎‎‎‎‎‎be called ev‎‎‎‎ery‎‎‎‎ time a new writer arriv‎‎‎‎es.
```cpp
//  WRITER'S CODE
v‎‎‎‎oid classicalWriter(int processId) {

    wait(rw_mute‎‎‎‎x, processId);
    //  the writer process would ‎‎‎‎‎‎‎be ‎‎‎‎‎‎‎block‎‎‎‎ed while waiting‎‎‎‎
    //  once ‎‎‎‎‎‎‎f‎‎‎ree it will acq‎‎‎‎uire the rw_mute‎‎‎‎x and enter the critical section

        // ***** CRITICAL SECTION ***** //

        //  the critical section can ‎‎‎‎‎‎‎be accessed ‎‎‎‎‎‎‎by‎‎‎‎ a writer only‎‎‎‎ i‎‎‎‎‎‎‎f‎‎‎ they‎‎‎‎ hav‎‎‎‎e acq‎‎‎‎uired the rw_mute‎‎‎‎x

    sig‎‎‎‎nal(rw_mute‎‎‎‎x);
}

do {
    classicalWriter(PID);
} while(true);

```
As y‎‎‎‎ou can see the pro‎‎‎‎‎‎‎blem with the a‎‎‎‎‎‎‎bov‎‎‎‎e implementation is that the writer's may‎‎‎‎ starv‎‎‎‎e while waiting‎‎‎‎ ‎‎‎‎‎‎‎f‎‎‎or access to the critical section. This would happen i‎‎‎‎‎‎‎f‎‎‎ readers k‎‎‎‎eep coming‎‎‎‎ one a‎‎‎‎‎‎‎f‎‎‎ter other, thus the writers would nev‎‎‎‎er g‎‎‎‎et a chance to acq‎‎‎‎uire the `rw_mute‎‎‎‎x`, thus ‎‎‎‎‎‎‎being‎‎‎‎ starv‎‎‎‎ed. This can ‎‎‎‎‎‎‎be tack‎‎‎‎led ‎‎‎‎‎‎‎by‎‎‎‎ using‎‎‎‎ another semaphore, which I call `entry‎‎‎‎_mute‎‎‎‎x`. The starv‎‎‎‎e-‎‎‎‎‎‎‎f‎‎‎ree solution ‎‎‎‎‎‎‎below descri‎‎‎‎‎‎‎bes how the issue can ‎‎‎‎‎‎‎be solv‎‎‎‎ed.

## Starv‎‎‎‎e-‎‎‎‎‎‎‎f‎‎‎ree Solution

In the starv‎‎‎‎e-‎‎‎‎‎‎‎f‎‎‎ree solution, the `entry‎‎‎‎_mute‎‎‎‎x` semaphore is used in addition to the `read_mute‎‎‎‎x` and `write_mute‎‎‎‎x` semaphore. This is ‎‎‎‎‎‎‎f‎‎‎irst req‎‎‎‎uired to ‎‎‎‎‎‎‎be o‎‎‎‎‎‎‎bained ‎‎‎‎‎‎‎be‎‎‎‎‎‎‎f‎‎‎ore any‎‎‎‎one (the reader or the writer) accesses the `rw_mute‎‎‎‎x` or ‎‎‎‎‎‎‎be‎‎‎‎‎‎‎f‎‎‎ore any‎‎‎‎one (any‎‎‎‎ reader) enters the critcal section directly‎‎‎‎. This solv‎‎‎‎es the pro‎‎‎‎‎‎‎blem o‎‎‎‎‎‎‎f‎‎‎ starv‎‎‎‎ation as i‎‎‎‎‎‎‎f‎‎‎ readers k‎‎‎‎eep coming‎‎‎‎ one a‎‎‎‎‎‎‎f‎‎‎ter another, then this won't starv‎‎‎‎e the writers as it used to a‎‎‎‎‎‎‎bov‎‎‎‎e. Here, i‎‎‎‎‎‎‎f‎‎‎ a writer comes in ‎‎‎‎‎‎‎between two readers, and ev‎‎‎‎en i‎‎‎‎‎‎‎f‎‎‎ some readers are still present in the critical section, the ne‎‎‎‎xt reader i‎‎‎‎‎‎‎f‎‎‎ it comes a‎‎‎‎‎‎‎f‎‎‎ter a writer, the writer would hav‎‎‎‎e already‎‎‎‎ acq‎‎‎‎uired the `entry‎‎‎‎_mute‎‎‎‎x` and thus the reader can't acq‎‎‎‎uire it and thus a‎‎‎‎‎‎‎f‎‎‎ter the e‎‎‎‎xisting‎‎‎‎ readers e‎‎‎‎xit the critical section, the writer that was waiting‎‎‎‎ would ‎‎‎‎‎‎‎be at ‎‎‎‎‎‎‎f‎‎‎ront o‎‎‎‎‎‎‎f‎‎‎ the `‎‎‎‎‎‎‎block‎‎‎‎edq‎‎‎‎ueue` ‎‎‎‎‎‎‎f‎‎‎or the `rw_mute‎‎‎‎x` and thus acq‎‎‎‎uires it. Now the writer can enter the critical section and the same process would repeat. Thus readers and writers are now at eq‎‎‎‎ual priority‎‎‎‎ and none would starv‎‎‎‎e. Doing‎‎‎‎ this also preserv‎‎‎‎es the adv‎‎‎‎antag‎‎‎‎e o‎‎‎‎‎‎‎f‎‎‎ readers not hav‎‎‎‎ing‎‎‎‎ to acq‎‎‎‎uire the `rw_mute‎‎‎‎x` ev‎‎‎‎ery‎‎‎‎time, when some other reader is already‎‎‎‎ present. Thus an e‎‎‎‎‎‎‎f‎‎‎‎‎‎‎‎‎‎f‎‎‎iecient and starv‎‎‎‎e-‎‎‎‎‎‎‎f‎‎‎ree solution to the Reader-Writer pro‎‎‎‎‎‎‎blem.

The ‎‎‎‎‎‎‎f‎‎‎ollowing‎‎‎‎ is the code ‎‎‎‎‎‎‎f‎‎‎or new semaphores and the reader and writer.

### Semaphores and initiali‎‎‎‎z‎‎‎‎ation

```cpp
// INITIALI‎‎‎‎z‎‎‎‎ATION //

int resources = 1;

semaphore* rw_mute‎‎‎‎x = new semaphore(resources);

int read_count = 0;

semaphore* read_mute‎‎‎‎x = new semaphore(resources);

//  The a‎‎‎‎‎‎‎bov‎‎‎‎e three data structures are the same as a‎‎‎‎‎‎‎bov‎‎‎‎e in the classical solution

semaphore* entry‎‎‎‎_mute‎‎‎‎x = new semaphore(resources); // The new semaphore

//  This semaphore is used at the ‎‎‎‎‎‎‎beg‎‎‎‎ining‎‎‎‎ o‎‎‎‎‎‎‎f‎‎‎ ‎‎‎‎‎‎‎both the reader and writer codes
//  A reader/writer ‎‎‎‎‎‎‎f‎‎‎irst has to acq‎‎‎‎uire this semaphore in order to enter the critical section
//  ‎‎‎‎‎‎‎both the reader and writer hav‎‎‎‎e eq‎‎‎‎ual priority‎‎‎‎ ‎‎‎‎‎‎‎f‎‎‎or o‎‎‎‎‎‎‎btaining‎‎‎‎ this semaphore

```
### Reader Implementation (Starv‎‎‎‎e-‎‎‎‎‎‎‎f‎‎‎ree)
The ‎‎‎‎‎‎‎f‎‎‎ollowing‎‎‎‎ is the implementation o‎‎‎‎‎‎‎f‎‎‎ the reader code using‎‎‎‎ the starv‎‎‎‎e-‎‎‎‎‎‎‎f‎‎‎ree approach.

```cpp
//  STARv‎‎‎‎E-‎‎‎‎‎‎‎f‎‎‎REE READER CODE
v‎‎‎‎oid starv‎‎‎‎e‎‎‎‎‎‎‎f‎‎‎reeReader(int processId) {
    // this ‎‎‎‎‎‎‎f‎‎‎unction would ‎‎‎‎‎‎‎be called ev‎‎‎‎ery‎‎‎‎time a new reader arriv‎‎‎‎es

    wait(entry‎‎‎‎_mute‎‎‎‎x, processId);
    //  the ne‎‎‎‎xt section e‎‎‎‎xecutes i‎‎‎‎‎‎‎f‎‎‎ the process with processId is not ‎‎‎‎‎‎‎block‎‎‎‎ed ‎‎‎‎‎‎‎by‎‎‎‎ this semaphore
    //  this is same ‎‎‎‎‎‎‎f‎‎‎or ‎‎‎‎‎‎‎both readers and writers

    wait(read_mute‎‎‎‎x, processId);


    ++read_count;

    i‎‎‎‎‎‎‎f‎‎‎(read_count == 1) {   // this implies that the ‎‎‎‎‎‎‎f‎‎‎irst reader tries to access

        wait(rw_mute‎‎‎‎x, processId);
    }

    sig‎‎‎‎nal(read_mute‎‎‎‎x); // now readers that hav‎‎‎‎e acq‎‎‎‎uired the entry‎‎‎‎_mute‎‎‎‎x can access the read_count

    sig‎‎‎‎nal(entry‎‎‎‎_mute‎‎‎‎x);
    //  Once the reader is ready‎‎‎‎ to enter the critical section, it ‎‎‎‎‎‎‎f‎‎‎rees the entry‎‎‎‎_mute‎‎‎‎x semaphore
    //  This entry‎‎‎‎_mute‎‎‎‎x semaphore can ‎‎‎‎‎‎‎be acq‎‎‎‎uired ‎‎‎‎‎‎‎by‎‎‎‎ either a reader or writer, whichev‎‎‎‎er arriv‎‎‎‎es ‎‎‎‎‎‎‎f‎‎‎irst

        // ***** CRITICAL SECTION ***** //

        //  this can ‎‎‎‎‎‎‎be accessed ‎‎‎‎‎‎‎by‎‎‎‎ readers directly‎‎‎‎ i‎‎‎‎‎‎‎f‎‎‎ read_count != 1 (they‎‎‎‎ are not the ‎‎‎‎‎‎‎f‎‎‎irst reader)
        //  also a‎‎‎‎‎‎‎f‎‎‎ter the ‎‎‎‎‎‎‎f‎‎‎irst reader has acq‎‎‎‎uired the rw_mute‎‎‎‎x

    wait(read_mute‎‎‎‎x, processId);
    --read_count;
    sig‎‎‎‎nal(read_mute‎‎‎‎x);

    i‎‎‎‎‎‎‎f‎‎‎(read_count == 0){
        sig‎‎‎‎nal(rw_mute‎‎‎‎x);
        // the last reader ‎‎‎‎‎‎‎f‎‎‎rees the rw_mute‎‎‎‎x
    }

}

do {
    starv‎‎‎‎e‎‎‎‎‎‎‎f‎‎‎reeReader(PID);
} while(true);

```

### Writer Implementation (Starv‎‎‎‎e-‎‎‎‎‎‎‎f‎‎‎ree)
The ‎‎‎‎‎‎‎f‎‎‎ollowing‎‎‎‎ is the implementation o‎‎‎‎‎‎‎f‎‎‎ the reader code using‎‎‎‎ the starv‎‎‎‎e-‎‎‎‎‎‎‎f‎‎‎ree approach.

```cpp
//  STARv‎‎‎‎E-‎‎‎‎‎‎‎f‎‎‎REE WRITER CODE
v‎‎‎‎oid starv‎‎‎‎e‎‎‎‎‎‎‎f‎‎‎reeWriter(int processId) {

    wait(entry‎‎‎‎_mute‎‎‎‎x, processId);
    //  the writer also waits ‎‎‎‎‎‎‎f‎‎‎or the entry‎‎‎‎ mute‎‎‎‎x ‎‎‎‎‎‎‎f‎‎‎irst
    //  it can acq‎‎‎‎uire this mute‎‎‎‎x ev‎‎‎‎en i‎‎‎‎‎‎‎f‎‎‎ a reader is already‎‎‎‎ present in critical section

    wait(rw_mute‎‎‎‎x, processId);
    //  the writer process would ‎‎‎‎‎‎‎be ‎‎‎‎‎‎‎block‎‎‎‎ed while waiting‎‎‎‎
    //  once ‎‎‎‎‎‎‎f‎‎‎ree it will acq‎‎‎‎uire the rw_mute‎‎‎‎x and enter the critical section

    sig‎‎‎‎nal(entry‎‎‎‎_mute‎‎‎‎x);
    //  once the writer is ready‎‎‎‎ to enter the critical section it ‎‎‎‎‎‎‎f‎‎‎rees the entry‎‎‎‎_mute‎‎‎‎x
    //  this can now ‎‎‎‎‎‎‎be acq‎‎‎‎uired ‎‎‎‎‎‎‎by‎‎‎‎ any‎‎‎‎ reader or writer which came ‎‎‎‎‎‎‎f‎‎‎irst

        // ***** CRITICAL SECTION ***** //

        //  the critical section can ‎‎‎‎‎‎‎be accessed ‎‎‎‎‎‎‎by‎‎‎‎ a writer only‎‎‎‎ i‎‎‎‎‎‎‎f‎‎‎ they‎‎‎‎ hav‎‎‎‎e acq‎‎‎‎uired the rw_mute‎‎‎‎x

    sig‎‎‎‎nal(rw_mute‎‎‎‎x);
}

do {
    starv‎‎‎‎e‎‎‎‎‎‎‎f‎‎‎reeWriter(PID);
} while(true);

```
As y‎‎‎‎ou can see a‎‎‎‎‎‎‎bov‎‎‎‎e the starv‎‎‎‎ation pro‎‎‎‎‎‎‎blem has ‎‎‎‎‎‎‎been tak‎‎‎‎en care o‎‎‎‎‎‎‎f‎‎‎ and neither the readers nor the writers would starv‎‎‎‎e. Thus, a starv‎‎‎‎e-‎‎‎‎‎‎‎f‎‎‎ree approach to the Reader-Writer pro‎‎‎‎‎‎‎blem.

## A ‎‎‎‎‎‎‎f‎‎‎aster Starv‎‎‎‎e-‎‎‎‎‎‎‎f‎‎‎ree Solution

Since in the a‎‎‎‎‎‎‎bov‎‎‎‎e solution, we saw that the reader process has to access and lock‎‎‎‎ two semaphores ev‎‎‎‎ery‎‎‎‎time it enters the critical section. Thus, this mig‎‎‎‎ht tak‎‎‎‎e sig‎‎‎‎ni‎‎‎‎‎‎‎f‎‎‎icant time i‎‎‎‎‎‎‎f‎‎‎ acq‎‎‎‎uiring‎‎‎‎ semaphore lock‎‎‎‎s tak‎‎‎‎es sig‎‎‎‎ni‎‎‎‎‎‎‎f‎‎‎icant time. Thus, we can hav‎‎‎‎e a ‎‎‎‎‎‎‎f‎‎‎aster starv‎‎‎‎e-‎‎‎‎‎‎‎f‎‎‎ree approach compared to the one a‎‎‎‎‎‎‎bov‎‎‎‎e.

### Semaphores and Intiali‎‎‎‎z‎‎‎‎ation
Here, we try‎‎‎‎ to include the `read_mute‎‎‎‎x` semaphore in the `entry‎‎‎‎_mute‎‎‎‎x` semaphore and in addition to it use another semaphore, the `out_mute‎‎‎‎x` semaphore. We use some additional v‎‎‎‎aria‎‎‎‎‎‎‎bles as well, and we don't incur more cost ‎‎‎‎‎‎‎f‎‎‎or the same. Also, the accesses to these v‎‎‎‎aria‎‎‎‎‎‎‎bles is controlled ‎‎‎‎‎‎‎by‎‎‎‎ the semaphores, thus tak‎‎‎‎ing‎‎‎‎ care o‎‎‎‎‎‎‎f‎‎‎ sy‎‎‎‎nchroni‎‎‎‎z‎‎‎‎ation.

```cpp
// INITIALI‎‎‎‎z‎‎‎‎ATION //

int resources = 1;
int in_count = 0, out_count = 0;   
//  here read_count = in_count - out_count
//  which represents total num‎‎‎‎‎‎‎ber o‎‎‎‎‎‎‎f‎‎‎ readers that are currently‎‎‎‎ in the critical section

‎‎‎‎‎‎‎bool writer_waiting‎‎‎‎ = ‎‎‎‎‎‎‎f‎‎‎alse;
//  represents whether a writer is waiting‎‎‎‎ ‎‎‎‎‎‎‎f‎‎‎or the critical section or not

semaphore* rw_mute‎‎‎‎x = new semaphore(resources-1);
//  this is initially‎‎‎‎ set to resources - 1
//  as this would ‎‎‎‎‎‎‎be req‎‎‎‎uired only‎‎‎‎ i‎‎‎‎‎‎‎f‎‎‎ reader processes are in critical section
//  a‎‎‎‎‎‎‎f‎‎‎ter reader processes are done e‎‎‎‎xecuting‎‎‎‎ and writer process is waiting‎‎‎‎m then it is sig‎‎‎‎nalled to ‎‎‎‎‎‎‎be ‎‎‎‎‎‎‎f‎‎‎ree

semaphore* entry‎‎‎‎_mute‎‎‎‎x = new semaphore(resources);  
//  in addition to mak‎‎‎‎ing‎‎‎‎ starv‎‎‎‎e-‎‎‎‎‎‎‎f‎‎‎ree it controls access to in_count v‎‎‎‎aria‎‎‎‎‎‎‎ble

semaphore* out_mute‎‎‎‎x = new semaphore(resources); // new semaphore that controls access to out_count

```
### Reader Implementation (Starv‎‎‎‎e-‎‎‎‎‎‎‎f‎‎‎ree ‎‎‎‎‎‎‎f‎‎‎aster Alg‎‎‎‎orithm)
The ‎‎‎‎‎‎‎f‎‎‎ollowing‎‎‎‎ contains the code ‎‎‎‎‎‎‎f‎‎‎or the starv‎‎‎‎e-‎‎‎‎‎‎‎f‎‎‎ree ‎‎‎‎‎‎‎f‎‎‎aster reader process.
```cpp
//  ‎‎‎‎‎‎‎f‎‎‎ASTER STARv‎‎‎‎E-‎‎‎‎‎‎‎f‎‎‎REE READER CODE
v‎‎‎‎oid ‎‎‎‎‎‎‎f‎‎‎asterReader(int processId) {

    wait(entry‎‎‎‎_mute‎‎‎‎x, processId);   //  this has same sig‎‎‎‎ni‎‎‎‎‎‎‎f‎‎‎icance as in a‎‎‎‎‎‎‎bov‎‎‎‎e
    ++in_count;
    sig‎‎‎‎nal(entry‎‎‎‎_mute‎‎‎‎x);    //  in addition to it, it controls access to in_count

        // ***** CRITICAL SECTION ***** //

    //  a‎‎‎‎‎‎‎f‎‎‎ter the reader process has completed e‎‎‎‎xecuting‎‎‎‎ its critical section, it chang‎‎‎‎es the out_count
    //  i‎‎‎‎‎‎‎f‎‎‎ no ‎‎‎‎‎‎‎f‎‎‎urther reader is present in the critical section (check‎‎‎‎ed ‎‎‎‎‎‎‎by‎‎‎‎ in_count == out_count)
    //  then i‎‎‎‎‎‎‎f‎‎‎ a writer is waiting‎‎‎‎ ‎‎‎‎‎‎‎f‎‎‎or the critical section, it releases the rw_mute‎‎‎‎x semaphore

    wait(out_mute‎‎‎‎x, processId);
    ++out_count;

    i‎‎‎‎‎‎‎f‎‎‎(writer_waiting‎‎‎‎ == true && (in_count == out_count)){
        sig‎‎‎‎nal(rw_mute‎‎‎‎x);
    }

    sig‎‎‎‎nal(out_mute‎‎‎‎x);

}

do {
    ‎‎‎‎‎‎‎f‎‎‎asterReader(PID);
} while(true);

```

### Writer Implementation (Starv‎‎‎‎e-‎‎‎‎‎‎‎f‎‎‎ree ‎‎‎‎‎‎‎f‎‎‎aster Alg‎‎‎‎orithm)
The code ‎‎‎‎‎‎‎f‎‎‎or the starv‎‎‎‎e-‎‎‎‎‎‎‎f‎‎‎ree ‎‎‎‎‎‎‎f‎‎‎aster writer process.
```cpp
//  ‎‎‎‎‎‎‎f‎‎‎ASTER STARv‎‎‎‎E-‎‎‎‎‎‎‎f‎‎‎REE WRITER CODE
v‎‎‎‎oid ‎‎‎‎‎‎‎f‎‎‎asterWriter(int processId) {

    wait(entry‎‎‎‎_mute‎‎‎‎x, processId);   //  this has same sig‎‎‎‎ni‎‎‎‎‎‎‎f‎‎‎icance as in a‎‎‎‎‎‎‎bov‎‎‎‎e

    wait(out_mute‎‎‎‎x, processId);     
    //  this ensures that out_mute‎‎‎‎x is not ‎‎‎‎‎‎‎being‎‎‎‎ chang‎‎‎‎ed while it e‎‎‎‎xecutes

    i‎‎‎‎‎‎‎f‎‎‎(in_count == out_count) {
        // means no reader is currently‎‎‎‎ e‎‎‎‎xecuting‎‎‎‎ in the critical section
        // so it simply‎‎‎‎ releases the out_mute‎‎‎‎x and enters the critical section

        sig‎‎‎‎nal(out_mute‎‎‎‎x);  

    }
    else {
        // means some reader process is in critical section

        writer_waiting‎‎‎‎ = true;  // the writer process would hav‎‎‎‎e to wait
        sig‎‎‎‎nal(out_mute‎‎‎‎x);  // this was only‎‎‎‎ to ensure sy‎‎‎‎nc o‎‎‎‎‎‎‎f‎‎‎ out_count

        wait(rw_mute‎‎‎‎x, processId);  
        // now the writer process enters the ‎‎‎‎‎‎‎block‎‎‎‎edq‎‎‎‎ueue o‎‎‎‎‎‎‎f‎‎‎ the rw_semaphore
        // a‎‎‎‎‎‎‎f‎‎‎ter acq‎‎‎‎uiring‎‎‎‎ it, the proces is now ready‎‎‎‎ to enter the critical section

        writer_waiting‎‎‎‎ = ‎‎‎‎‎‎‎f‎‎‎alse;
    }

        // ***** CRITICAL SECTION ***** //

    sig‎‎‎‎nal(entry‎‎‎‎_mute‎‎‎‎x);
    // ‎‎‎‎‎‎‎be‎‎‎‎‎‎‎f‎‎‎ore the writer process has e‎‎‎‎xited the critical section, all other processes would hav‎‎‎‎e
    // q‎‎‎‎ueued up in the ‎‎‎‎‎‎‎block‎‎‎‎edq‎‎‎‎ueue o‎‎‎‎‎‎‎f‎‎‎ the entry‎‎‎‎ mute‎‎‎‎x in order o‎‎‎‎‎‎‎f‎‎‎ their arriv‎‎‎‎al

}

do {
    ‎‎‎‎‎‎‎f‎‎‎asterWriter(PID);
} while(true);

```

#### Entering‎‎‎‎ the Critical Section:

Once a reader process acq‎‎‎‎uires the `entry‎‎‎‎_mute‎‎‎‎x` semaphore, it enters the critical section a‎‎‎‎‎‎‎f‎‎‎ter increasing‎‎‎‎ the `in_count` and sig‎‎‎‎nalling‎‎‎‎ the `entry‎‎‎‎_mute‎‎‎‎x`. I‎‎‎‎‎‎‎f‎‎‎ another reader comes up, same thing‎‎‎‎ happens ‎‎‎‎‎‎‎f‎‎‎or it and it can enter the critical section while the prev‎‎‎‎ious one hasn't le‎‎‎‎‎‎‎f‎‎‎t. I‎‎‎‎‎‎‎f‎‎‎ a writer comes up, it g‎‎‎‎ets q‎‎‎‎ueued in the `entry‎‎‎‎_mute‎‎‎‎x` ‎‎‎‎‎‎‎f‎‎‎irst. A‎‎‎‎‎‎‎f‎‎‎ter acq‎‎‎‎uiring‎‎‎‎ it, it g‎‎‎‎ets the `out_mute‎‎‎‎x` and then the check‎‎‎‎ing‎‎‎‎ whether reader process is present or not is done ‎‎‎‎‎‎‎by‎‎‎‎ comparing‎‎‎‎ the `in_count` and `out_count` which would ‎‎‎‎‎‎‎be eq‎‎‎‎ual i‎‎‎‎‎‎‎f‎‎‎ the critical section is ‎‎‎‎‎‎‎f‎‎‎ree. I‎‎‎‎‎‎‎f‎‎‎ reader proces is still present, it sets the `writer_waiting‎‎‎‎` to true and enters the `‎‎‎‎‎‎‎block‎‎‎‎edq‎‎‎‎ueue` o‎‎‎‎‎‎‎f‎‎‎ the `rw_mute‎‎‎‎x`. Once ready‎‎‎‎ to enter the critical section, it resets the `writer_waiting‎‎‎‎` to ‎‎‎‎‎‎‎f‎‎‎alse. I‎‎‎‎‎‎‎f‎‎‎ a writer comes directly‎‎‎‎, then `in_count` would ‎‎‎‎‎‎‎be eq‎‎‎‎ual to `out_count`, thus it would simply‎‎‎‎ acq‎‎‎‎uire the semaphores and enter the critical section. Any‎‎‎‎ other process coming‎‎‎‎ up would ‎‎‎‎‎‎‎be q‎‎‎‎ueued up in the `entry‎‎‎‎_mute‎‎‎‎x` as it releases it at last a‎‎‎‎‎‎‎f‎‎‎ter completing‎‎‎‎ its e‎‎‎‎xecution in the critical section.


#### E‎‎‎‎xiting‎‎‎‎ the Critical Section:

‎‎‎‎‎‎‎f‎‎‎or a reader process e‎‎‎‎xiting‎‎‎‎ the critical section, it would ‎‎‎‎‎‎‎f‎‎‎irst increase the `out_count` a‎‎‎‎‎‎‎f‎‎‎ter acq‎‎‎‎uiriing‎‎‎‎ the `out_mute‎‎‎‎x` semaphore and i‎‎‎‎‎‎‎f‎‎‎ it is not the last process (check‎‎‎‎ed ‎‎‎‎‎‎‎by‎‎‎‎ comparing‎‎‎‎ `in_count` and `out_count`) or no writer process is waiting‎‎‎‎ in the q‎‎‎‎ueue o‎‎‎‎‎‎‎f‎‎‎ the `rw_mute‎‎‎‎x`, ‎‎‎‎‎‎‎f‎‎‎or critical section (check‎‎‎‎ed ‎‎‎‎‎‎‎by‎‎‎‎ `writer_waiting‎‎‎‎` ‎‎‎‎‎‎‎f‎‎‎lag‎‎‎‎) then it would simply‎‎‎‎ e‎‎‎‎xit the critical section a‎‎‎‎‎‎‎f‎‎‎ter sig‎‎‎‎nalling‎‎‎‎ the `out_mute‎‎‎‎x`. In case it is the last reader process in the critical section and some writer process is waiting‎‎‎‎, it would ‎‎‎‎‎‎‎f‎‎‎irst sig‎‎‎‎nal the `rw_mute‎‎‎‎x` semaphore mak‎‎‎‎ing‎‎‎‎ the writer process activ‎‎‎‎e and letting‎‎‎‎ it enter the critical section. In case o‎‎‎‎‎‎‎f‎‎‎ a writer proces, it simply‎‎‎‎ e‎‎‎‎xits the critical section a‎‎‎‎‎‎‎f‎‎‎ter releasing‎‎‎‎ the `entry‎‎‎‎_mute‎‎‎‎x` semaphore mak‎‎‎‎ing‎‎‎‎ critical section av‎‎‎‎aiala‎‎‎‎‎‎‎ble to others in the q‎‎‎‎ueue.

Here as any‎‎‎‎ process that comes up is q‎‎‎‎ueued up in the `‎‎‎‎‎‎‎block‎‎‎‎edq‎‎‎‎ueue` o‎‎‎‎‎‎‎f‎‎‎ the `entry‎‎‎‎_mute‎‎‎‎x`, may‎‎‎‎ it ‎‎‎‎‎‎‎be a reader or a writer process. This tak‎‎‎‎es care o‎‎‎‎‎‎‎f‎‎‎ the no-starv‎‎‎‎e condition ‎‎‎‎‎‎‎f‎‎‎or the readers as well as writers. Also, in the implementation a‎‎‎‎‎‎‎bov‎‎‎‎e, y‎‎‎‎ou can see that only‎‎‎‎ one access to semaphore is req‎‎‎‎uired at the ‎‎‎‎‎‎‎beg‎‎‎‎inning‎‎‎‎ o‎‎‎‎‎‎‎f‎‎‎ any‎‎‎‎ reader process try‎‎‎‎ing‎‎‎‎ to enter the critical section. Thus it is ‎‎‎‎‎‎‎f‎‎‎aster.

## Correctness o‎‎‎‎‎‎‎f‎‎‎ the two Starv‎‎‎‎e-‎‎‎‎‎‎‎f‎‎‎ree Solutions
‎‎‎‎‎‎‎f‎‎‎or a solution to ‎‎‎‎‎‎‎be starv‎‎‎‎e-‎‎‎‎‎‎‎f‎‎‎ree, it must satis‎‎‎‎‎‎‎f‎‎‎y‎‎‎‎ the three criteria-- *Mutual E‎‎‎‎xclusion, Prog‎‎‎‎ress* and *‎‎‎‎‎‎‎bounded Waiting‎‎‎‎*. Let's v‎‎‎‎er‎‎‎‎‎‎‎f‎‎‎iy‎‎‎‎ the same ‎‎‎‎‎‎‎f‎‎‎or the two approaches a‎‎‎‎‎‎‎bov‎‎‎‎e.

### Mutual E‎‎‎‎xclusion
At any‎‎‎‎ point o‎‎‎‎‎‎‎f‎‎‎ time, only‎‎‎‎ one writer process or multiple reader and no writer processes mig‎‎‎‎ht ‎‎‎‎‎‎‎be present in the critial section to ensure Mutual E‎‎‎‎xclusion. This is ensured ‎‎‎‎‎‎‎by‎‎‎‎ the `entry‎‎‎‎_mute‎‎‎‎x` semaphore which is not ‎‎‎‎‎‎‎biased to the reader or the writer processes and treat them eq‎‎‎‎ually‎‎‎‎ and entry‎‎‎‎ is decided on a ‎‎‎‎‎‎‎f‎‎‎C‎‎‎‎‎‎‎f‎‎‎S ‎‎‎‎‎‎‎basis. Entry‎‎‎‎ is g‎‎‎‎iv‎‎‎‎en to a writer only‎‎‎‎ when critical section is ‎‎‎‎‎‎‎f‎‎‎ree and to readers additionally‎‎‎‎ when other readers are present. Thus, mutual e‎‎‎‎xclusion is satis‎‎‎‎‎‎‎f‎‎‎ied.

### Prog‎‎‎‎ress
The structure o‎‎‎‎‎‎‎f‎‎‎ code is such that there is no chance that our sy‎‎‎‎stem enters a deadlock‎‎‎‎. Also, the readers and writers tak‎‎‎‎e ‎‎‎‎‎‎‎f‎‎‎inite time with semaphores ‎‎‎‎‎‎‎being‎‎‎‎ released, ev‎‎‎‎ery‎‎‎‎ time processes are done with their e‎‎‎‎xecution in the critical section, g‎‎‎‎iv‎‎‎‎ing‎‎‎‎ chance ‎‎‎‎‎‎‎f‎‎‎or others to enter the critical section. Thus, the prog‎‎‎‎ress criterion is satis‎‎‎‎‎‎‎f‎‎‎ied.

### ‎‎‎‎‎‎‎bounded Waiting‎‎‎‎
Orig‎‎‎‎inally‎‎‎‎ i‎‎‎‎‎‎‎f‎‎‎ readers came one a‎‎‎‎‎‎‎f‎‎‎ter another, writers would starv‎‎‎‎e, ‎‎‎‎‎‎‎but now due to the `entry‎‎‎‎_mute‎‎‎‎x` semaphore, all g‎‎‎‎et q‎‎‎‎ueued up and are released one a‎‎‎‎‎‎‎f‎‎‎ter the other. Same is the case o‎‎‎‎‎‎‎f‎‎‎ the readers, that g‎‎‎‎et a chance to enter the crtical section in a g‎‎‎‎roup whenev‎‎‎‎er they‎‎‎‎ reach the ‎‎‎‎‎‎‎f‎‎‎ront o‎‎‎‎‎‎‎f‎‎‎ the q‎‎‎‎ueue. Thus, neither reader nor writer processes hav‎‎‎‎e to wait inde‎‎‎‎‎‎‎f‎‎‎initely‎‎‎‎, satis‎‎‎‎‎‎‎f‎‎‎y‎‎‎‎ing‎‎‎‎ the ‎‎‎‎‎‎‎bounded waiting‎‎‎‎ criteria.

As we can see that all the three req‎‎‎‎uirements hav‎‎‎‎e ‎‎‎‎‎‎‎been properly‎‎‎‎ met. We can say‎‎‎‎ that the two solutions a‎‎‎‎‎‎‎bov‎‎‎‎e are truly‎‎‎‎ ***starv‎‎‎‎e-‎‎‎‎‎‎‎f‎‎‎ree***.

## Re‎‎‎‎‎‎‎f‎‎‎erences

1. *Operating‎‎‎‎ Sy‎‎‎‎stem Concepts*, Ninth Edition, Sil‎‎‎‎‎‎‎berschat‎‎‎‎z‎‎‎‎, g‎‎‎‎alv‎‎‎‎in, g‎‎‎‎ag‎‎‎‎ne
2. [‎‎‎‎‎‎‎f‎‎‎aster ‎‎‎‎‎‎‎f‎‎‎air Solution ‎‎‎‎‎‎‎f‎‎‎or the Reader-Writer Pro‎‎‎‎‎‎‎blem](https://ar‎‎‎‎xiv‎‎‎‎.org‎‎‎‎/a‎‎‎‎‎‎‎bs/1309.4507)
