![[Pasted image 20240505145422.png]]

![[Pasted image 20240505145958.png]]
![[Pasted image 20240505150034.png]]
![[Pasted image 20240505150119.png]]
![[Pasted image 20240505150128.png]]

Zookeeper - отлично подходит для чтения(очень быстрый), но не для записи

!![[Pasted image 20240505151205.png]]

![[Pasted image 20240505152748.png]]


![[Pasted image 20240505153118.png]]

Режими отправик
![[Pasted image 20240505153320.png]]
acks = 0 - мы не требуем подтверждения отправки(самый ненадежный режим)

acks = 1 - Producer ждет подтверждения отправки сообщений
![[Pasted image 20240505153518.png]]

acks = all. Ждем сообщения от всех ISR
![[Pasted image 20240505153533.png]]
