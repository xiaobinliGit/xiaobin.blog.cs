|调用进程|被调用的操作|信号量状态||
|:--|:--|:--|:--|
|1. |P3|pickup|IM.mutex=1; next=0; next_count=0; self[i]=0; self_count[i]=0; state[i]=thinking;|
|2. |P3|enter(IM)|IM.mutex=0; next=0; next_count=0; self[i]=0; self_count[i]=0; state[i]=thinking;|
|3. |P3|State[3]=hungry|IM.mutex=0; next=0; next_count=0; self[i]=0; self_count[i]=0; state[i]=thinking; state[3]=hungry;|
|4. |P3|test(3)|IM.mutex=0; next=0; next_count=0; self[i]=0; self_count[i]=0; state[i]=thinking; state[3]=hungry;|
|5. |P3|State[3]=eating|IM.mutex=0; next=0; next_count=0; self[i]=0; self_count[i]=0; state[i]=thinking; state[3]= eating;|
|6. |P3|Signal(self[3])|IM.mutex=0; next=0; next_count=0; self[i]=0; self_count[i]=0; state[i]=thinking; state[3]= eating;|
|||//空操作||
|7. |P3|leave(IM)|IM.mutex=1; next=0; next_count=0; self[i]=0; self_count[i]=0; state[i]=thinking; state[3]= eating;|
|8. |P1|pickup|IM.mutex=1; next=0; next_count=0; self[i]=0; self_count[i]=0; state[i]=thinking; state[3]= eating;|
|9. |P1|enter(IM)|IM.mutex=0; next=0; next_count=0; self[i]=0; self_count[i]=0; state[i]=thinking; state[3]= eating;|
|10. |P1|State[1]=hungry|IM.mutex=0; next=0; next_count=0; self[i]=0; self_count[i]=0; state[i]=thinking; state[3]= eating; state[1]=hungry;|
|11. |P1|test(1)|IM.mutex=0; next=0; next_count=0; self[i]=0; self_count[i]=0; state[i]=thinking; state[3]= eating; state[1]=hungry;|
|12. |P1|State[1]=eating|IM.mutex=0; next=0; next_count=0; self[i]=0; self_count[i]=0; state[i]=thinking; state[3]= eating; state[1]= eating;|
|13. |P1|Signal(self[1])|IM.mutex=0; next=0; next_count=0; self[i]=0; self_count[i]=0; state[i]=thinking; state[3]= eating; state[1]= eating;|
|||//空操作||
|14. |P3|leave(IM)|IM.mutex=1; next=0; next_count=0; self[i]=0; self_count[i]=0; state[i]=thinking; state[3]= eating; state[1]= eating;|
|15. |P2|pickup|IM.mutex=1; next=0; next_count=0; self[i]=0; self_count[i]=0; state[i]=thinking; state[3]= eating; state[1]= eating;|
|16. |P2|enter(IM)|IM.mutex=0; next=0; next_count=0; self[i]=0; self_count[i]=0; state[i]=thinking; state[3]= eating; state[1]= eating;|
|17. |P2|State[2]=hungry|IM.mutex=0; next=0; next_count=0; self[i]=0; self_count[i]=0; state[i]=thinking; state[3]= eating; state[1]= eating; state[2]= hungry;|
|18. |P2|test(2)|IM.mutex=0; next=0; next_count=0; self[i]=0; self_count[i]=0; state[i]=thinking; state[3]= eating; state[1]= eating; state[2]= hungry;|
|19. |P2|wait(self[2])|IM.mutex=1; next=0; next_count=0; self[i]=0; self[2]=-1 (P2); self_count[i]=0; self_count[2]=1; state[i]=thinking; state[3]=eating; state[1]= eating; state[2]= hungry;|
|||//||
|20. |P1|putdown|IM.mutex=1; next=0; next_count=0; self[i]=0; self[2]=-1 (P2); self_count[i]=0; self_count[2]=1; state[i]=thinking; state[3]=eating; state[1]= eating; state[2]= hungry;|
|21. |P1|enter(IM)|IM.mutex=0; next=0; next_count=0; self[i]=0; self[2]=-1 (P2); self_count[i]=0; self_count[2]=1; state[i]=thinking; state[3]=eating; state[1]= thinking; state[2]= hungry;|
|22. |P1|State[1]=thinking|IM.mutex=0; next=0; next_count=0; self[i]=0; self[2]=-1 (P2); self_count[i]=0; self_count[2]=1; state[i]=thinking; state[3]=eating; state[1]= thinking; state[2]= hungry;|
|23. |P1|test(0)|IM.mutex=0; next=0; next_count=0; self[i]=0; self[2]=-1 (P2); self_count[i]=0; self_count[2]=1; state[i]=thinking; state[3]=eating; state[1]= thinking; state[2]= hungry;|
|24. |P1|test(2)|IM.mutex=0; next=0; next_count=0; self[i]=0; self[2]=-1 (P2); self_count[i]=0; self_count[2]=1; state[i]=thinking; state[3]=eating; state[1]= thinking; state[2]= hungry;|
|25. |P1|leave(IM)|IM.mutex=1; next=0; next_count=0; self[i]=0; self[2]=-1 (P2); self_count[i]=0; self_count[2]=1; state[i]=thinking; state[3]=eating; state[1]= thinking; state[2]= hungry;|
|26. |P3|putdown|IM.mutex=1; next=0; next_count=0; self[i]=0; self[2]=-1 (P2); self_count[i]=0; self_count[2]=1; state[i]=thinking; state[3]=eating; state[1]= thinking; state[2]= hungry;|
|27. |P3|enter(IM)|IM.mutex=0; next=0; next_count=0; self[i]=0; self[2]=-1 (P2); self_count[i]=0; self_count[2]=1; state[i]=thinking; state[3]=eating; state[1]= thinking; state[2]= hungry;|
|28. |P3|State[3]=thinking|IM.mutex=0; next=0; next_count=0; self[i]=0; self[2]=-1 (P2); self_count[i]=0; self_count[2]=1; state[i]=thinking; state[2]= hungry;|
|29. |P3|test(2)|IM.mutex=0; next=0; next_count=0; self[i]=0; self[2]=-1 (P2); self_count[i]=0; self_count[2]=1; state[i]=thinking; state[2]= hungry;|
|||//序30, 31, 34||
|30. |P3|State[2]=eating|IM.mutex=0; next=0; next_count=0; self[i]=0; self[2]=-1 (P2); self_count[i]=0; self_count[2]=1; state[i]=thinking; state[2]= eating;|
|||//P3.test(2)中||
|31. |P3|Signal(self[2])|IM.mutex=0; next=-1 (P3); next_count=1; self[i]=0; self[2]=0 P2 (); self_count[i]=0; self_count[2]=1; state[i]=thinking; state[2]= eating;|
|||//P3.test(2)中||
|32. |P2|Self_count[2]—|IM.mutex=0; next=-1 (P3); next_count=1; self[i]=0; self_count[i]=0; self_count[2]=0; state[i]=thinking; state[2]= eating;|
|||//P2.P(wait)的末尾语句||
|33. |P2|leave(IM)|IM.mutex=0; next=0 P3 (); next_count=1; self[i]=0; self_count[i]=0; state[i]=thinking; state[2]= eating;|
|||//P2.pickup中的||
|34. |P3|next_count--|IM.mutex=0; next=0; next_count=0; self[i]=0; self_count[i]=0; state[i]=thinking; state[2]= eating;|
|||//P3.test(2)中的signal(self[2])的末尾语句||
|35. |P3|test(4)|IM.mutex=0; next=0; next_count=0; self[i]=0; self_count[i]=0; state[i]=thinking; state[2]= eating;|
|36. |P3|leave(IM)|IM.mutex=1; next=0; next_count=0; self[i]=0; self_count[i]=0; state[i]=thinking; state[2]= eating;|
|||//P3.putdwon的末尾语句||
|37. |P1|Pickup|IM.mutex=1; next=0; next_count=0; self[i]=0; self_count[i]=0; state[i]=thinking; state[2]= eating;|
|38. |P1|Enter(IM)|IM.mutex=0; next=0; next_count=0; self[i]=0; self_count[i]=0; state[i]=thinking; state[2]= eating;|
|39. |P1|State[1]=hungry|IM.mutex=0; next=0; next_count=0; self[i]=0; self_count[i]=0; self_count[2]=0; state[i]=thinking; state[1]=hungry; state[2]= eating;|
|40. |P1|Test(1)|IM.mutex=0; next=0; next_count=0; self[i]=0; self_count[i]=0; self_count[2]=0; state[i]=thinking; state[1]=hungry; state[2]= eating;|
|41. |P1|Wait(self[1])|IM.mutex=1; next=0; next_count=0; self[i]=0; self[1]=-1 (P1); self_count[i]=0; self_count[1]=1; state[i]=thinking; state[1]=hungry; state[2]= eating;|
|42. |P2|Putdown |IM.mutex=1; next=0; next_count=0; self[i]=0; self[1]=-1 (P1); self_count[i]=0; self_count[1]=1; state[i]=thinking; state[1]=hungry; state[2]= eating;|
|43. |P2|enter(IM)|IM.mutex=0; next=0; next_count=0; self[i]=0; self[1]=-1 (P1); self_count[i]=0; self_count[1]=1; state[i]=thinking; state[1]=hungry; state[2]= eating;|
|44. |P2|State[2]=thinking|IM.mutex=0; next=0; next_count=0; self[i]=0; self[1]=-1 (P1); self_count[i]=0; self_count[1]=1; state[i]=thinking; state[1]=hungry; state[2]= thinking;|
|45. |P2|test(1)|IM.mutex=0; next=0; next_count=0; self[i]=0; self[1]=-1 (P1); self_count[i]=0; self_count[1]=1; state[i]=thinking; state[1]=hungry; state[2]= thinking;|
|||//序||
|46. |P2|State[1]=eating|IM.mutex=0; next=0; next_count=0; self[i]=0; self[1]=-1 (P1); self_count[i]=0; self_count[1]=1; state[i]=thinking; state[1]=eating; state[2]= thinking;|
|||//P2.test(1)中||
|47. |P2|Signal(self[2])|IM.mutex=0; next=-1 (P2); next_count=1; self[i]=0; self[1]=0 P1 (); self_count[i]=0; self_count[1]=1; state[i]=thinking; state[1]=eating; state[2]= thinking;|
|||//P3.test(2)中||
|48. |P1|Self_count[1]—|IM.mutex=0; next=-1 (P2); next_count=1; self[i]=0; self[1]=0 P1 (); self_count[i]=0; self_count[1]=0; state[i]=thinking; state[1]=eating; state[2]= thinking;|
|||//P1.P(wait)的末尾语句||
|49. |P1|leave(IM)|IM.mutex=0; next=0 P2 (); next_count=1; self[i]=0; self[1]=0 P1 (); self_count[i]=0; self_count[1]=0; state[i]=thinking; state[1]=eating; state[2]= thinking;|
|||//P1.pickup中的||
|50. |P2|next_count--|IM.mutex=0; next=0; next_count=0; self[i]=0; self[1]=0 P1 (); self_count[i]=0; self_count[1]=0; state[i]=thinking; state[1]=eating; state[2]= thinking;|
|||//P2.test(1)中的signal(self[1])的末尾语句||
|51. |P2|test(3)|IM.mutex=0; next=0; next_count=0; self[i]=0; self[1]=0 P1 (); self_count[i]=0; self_count[1]=0; state[i]=thinking; state[1]=eating; state[2]= thinking;|
|52. |P2|leave(IM)|IM.mutex=1; next=0; next_count=0; self[i]=0; self[1]=0 P1 (); self_count[i]=0; self_count[1]=0; state[i]=thinki|
|||//P2.putdwon的末尾语句||
