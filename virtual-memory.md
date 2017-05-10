# 4. 虛擬記憶體

一個處理器的虛擬記憶體（virtual memory，VM）子系統實作了提供給每個行程的虛擬位址空間。這令每個行程都認為它是獨自在系統中的。虛擬記憶體的優點清單會在其它地方仔細地描述，所以這裡就不重複這些了。這一節會聚焦在虛擬記憶體子系統的實際的實作細節、以及與此相關的成本。

虛擬位址空間是由 CPU 的記憶體管理單元（Memory Management Unit，MMU）實作的。OS 必須填寫分頁表（page table）資料結構，但大多數 CPU 會自行做掉剩下的工作。這真的是個非常複雜的機制；理解它的最佳方式是引入使用的資料結構來描述虛擬位址空間。

由 MMU 實行的位址轉換的輸入為一個虛擬位址。它的值通常有極少量––如果有的話––的限制。在 32 位元系統上的虛擬位址為 32 位元的值，而在 64 位元系統上為 64 位元的值。在某些系統上，像是 x86 與 x86-64，使用的位址實際上牽涉到另一層級的間接性：這些架構使用了分段（segment），其只不過是將偏移量加到每個邏輯位址上。我們可以忽略位址產生過程的這個部分，它很瑣碎，而且就記憶體管理的效能而言，不是程式設計師必須要關心的東西。[^24]


[^24]: x86 上的分段限制是攸關效能的，但這又是另一個故事了。
