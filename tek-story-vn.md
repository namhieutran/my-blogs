## Trưởng thành qua Terminal

### 20 năm dùng Terminal

Có một việc rất quen thuộc mà sau hơn 20 năm làm IT, lần nào đổi máy, tui cũng làm đầu tiên. Không phải clone project, cũng chẳng phải cài IDE. Mà là… ngồi cả buổi chỉ để "độ" cái terminal.

Bắt đầu với Solaris; sau đó là Linux, Windows, với CMD và PowerShell; rồi nhảy qua macOS. 10 năm đầu, tui gần như không biết terminal có thể tùy biến, mở lên sao thì xài vậy.

Rồi tới thời làm macOS, bắt đầu biết iTerm2, Oh My Zsh, Powerlevel10k,... rồi plugin, theme, font, icon, animation, prompt... Cái gì trên Reddit nghe bảo đẹp là thử.

Terminal đúng là đẹp hơn.

Nhưng mỗi lần đổi máy… lại mở checklist, copy-paste, config, chỉnh, restart… lặp lại gần như nguyên ngày đầu tiên. Chưa kể, sao tui cứ thấy terminal chậm chậm, không nhanh như tool mặc định.

Có lẽ vấn đề không nằm ở terminal, mà ở cách tui tiếp cận việc setup.

### Một câu hỏi

Gần đây làm việc với CLI nhiều hơn, đặc biệt là các AI tools, lúc đó tui mới nhận ra một chuyện khá buồn cười: cái tui cần không phải một terminal đẹp lung linh, mà là một terminal phản hồi gần như ngay lập tức.

Một prompt chậm thêm 300-500 ms nghe có vẻ không đáng kể, nhưng nếu mỗi ngày mở vài trăm command thì cảm giác "khựng" đó xuất hiện liên tục. Nó không làm mất nhiều thời gian, nhưng nó làm mất nhịp suy nghĩ.

Hồi mới đi làm, tui thích nhìn terminal với thật nhiều thông tin. Bây giờ điều tui muốn chỉ còn là:

- Mở lên thật nhanh,
- Thấy thứ mình cần,
- Rồi quay lại giải quyết vấn đề.

Sau vài lần setup Windows cho home machine, macOS cho dev laptop, Linux VPS cho cloud server... Một câu hỏi xuất hiện:

> Mình có đang dành quá nhiều thời gian cho việc... chuẩn bị làm việc không?

> Nếu việc setup này cứ lặp đi lặp lại... Tại sao nó chưa được coi là một project?

Tui từng nghĩ mình đang tối ưu terminal cho đẹp, cho "ngầu", nhưng có vẻ tui chỉ đang tối ưu cảm giác… bận rộn.

### Dự án nhỏ thử nghiệm

Thế là thay vì nghĩ "cài terminal", tui thử coi nó là một dự án. Mà một dự án thì phải có: Goal - Output - Decision - Risk - Plan - Version

Với dự án nhỏ này, mọi thứ khá rõ ràng, với vài mục tiêu: 

- Setup máy mới dưới 30 phút
- Prompt phản hồi dưới 150ms
- Config có version
- Mọi thứ chạy lại được bằng Git
- Thêm tool mới dưới 2 phút

Sau vài vòng tìm hiểu, tui chốt: Ghostty • zsh • Starship • Homebrew • chezmoi • JetBrains Mono. Không phải vì "best", chỉ vì chúng phù hợp với tiêu chí của project.

Đến lúc implement, nhờ có tiêu chí "prompt <150ms", tui mới phát hiện một plugin đang làm terminal chậm đi khá nhiều. Nếu không đặt tiêu chí ngay từ đầu, có lẽ tui sẽ chẳng bao giờ để ý đến chi tiết này.

### Chứng minh ý tưởng lớn hơn

Kết thúc mini-project và nhìn lại, tui nhận ra cái mình học được nhiều nhất không phải "Ghostty tốt hơn terminal cũ", hay "bộ tool định dùng ngon", mà là việc chứng minh rằng khi buộc bản thân viết rõ:

- Mình muốn gì?
- Tiêu chí đánh giá là gì?
- Output là gì?

Thì rất nhiều giả định tưởng đúng lại hóa ra sai.

Terminal chỉ là dự án nhỏ đầu tiên. Điều tui thật sự muốn kiểm chứng là liệu cách làm này có thể áp dụng cho mọi việc hằng ngày hay không. Nếu ổn, biết đâu một ngày nào đó, phần lớn những việc lặp đi lặp lại sẽ không còn do tui làm nữa, mà sẽ do chính quy trình hoặc AI agent làm thay.

Trước đây tui tối ưu công cụ. Bây giờ tui tối ưu quy trình tạo ra công cụ.

Quy trình này… còn nữa… bài sau nha.
