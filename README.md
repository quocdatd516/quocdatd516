<html lang="vi">
<head>
<meta charset="UTF-8">
<title>Quản lý & Lọc Văn Bản</title>
<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.3/dist/css/bootstrap.min.css">
<style>
    body {
        font-family: "Times New Roman", serif;
        font-size: 16px;
        line-height: 1.5;
    }
	h2.text-center.text-primary.red-title {
		color: red;
		font-size: 26px;
		font-weight: bold;
		letter-spacing: 2px;
		width: 100%;
		margin: 20px auto;
		line-height: 1.4;
		color: #FFFF00;
	}
	
	h4.text-center.text-primary.red-title {
		font-size: 16px;
		font-weight: bold;
		letter-spacing: 2px;
		width: 70%;
		margin: 20px 0;
		line-height: 1.4;
		color: #FFFF00;
		text-align: left;
    }
    #quanly {
        background: linear-gradient(to bottom, #87ceeb, #e0f7ff);
        padding: 20px;
    }
    #loc {
        background-color: #99FFFF;
        padding: 20px;
    }
    table {
        width: 100%;
        border-collapse: collapse;
    }
    th, td {
        border: 1px solid #ccc;
        padding: 8px;
        text-align: center;
    }
    th {
        background-color: #f0f0f0;
    }
    .delete-btn {
        background: crimson;
        color: white;
        border: none;
        padding: 5px 10px;
        border-radius: 5px;
        cursor: pointer;
    }
    .nav-tabs .nav-link { font-weight: bold; }
	
	/* 🔹 Chữ chạy (CSS animation, thay cho <marquee>) */
	.marquee {
	    width: 100%;
	    overflow: hidden;
	    white-space: nowrap;
	    box-sizing: border-box;
	    background: #FF0000;
	    color: #FFFF00;
	    font-weight: bold;
	    padding: 0px 40px;
	    border-radius: 6px;
	    margin-top: 10px;
	}
	.marquee span {
	    display: inline-block;
	    padding-left: 100%;
	    animation: marquee 12s linear infinite;
	}
	.marquee:hover span { animation-play-state: paused; } /* tạm dừng khi rê chuột */

	@keyframes marquee {
     0%   { transform: translateX(0); }
     100% { transform: translateX(-100%); }
    }

    /* 🔹 Đồng hồ hiển thị ngày giờ */
    .clock {
     text-align: right;
     font-weight: bold;
     margin: 6px 0 0;
     color: #cc0000;
    }

    /* 🔹 Tỉ lệ độ rộng các cột (áp dụng cho cả 2 bảng ở TAB 1 & TAB 2) */
    table th:nth-child(1), table td:nth-child(1) { width: 5%; }
    table th:nth-child(2), table td:nth-child(2) { width: 15%; }
    table th:nth-child(3), table td:nth-child(3) { width: 40%; }
    table th:nth-child(4), table td:nth-child(4) { width: 15%; }
    table th:nth-child(5), table td:nth-child(5) { width: 15%; }
    table th:nth-child(6), table td:nth-child(6) { width: 10%; }

    .footer {
        background: #0044cc;
        color: white;
        text-align: center;
        padding: 4px;
        margin-top: 1px;
        line-height: 1.2;
        border-radius: 4px 4px 0 0;
        font-size: 14px;
    }
    .footer a {
        color: #ffeb3b;
        text-decoration: none;
    }
    .footer a:hover {
        text-decoration: underline;
    }
	
	#backToTopBtn {
        position: fixed;
        bottom: 20px;
        right: 20px;
        padding: 10px 15px;
        background: #007BFF;
        color: white;
        border: none;
        border-radius: 8px;
        cursor: pointer;
        display: none;
        transition: opacity 0.3s ease;
        z-index: 9999;
    }
    #backToTopBtn:hover {
        background: #0056b3;
    }

    /* CSS cho Modal */
    .modal {
        display: none;
        position: fixed;
        z-index: 10000;
        left: 0;
        top: 0;
        width: 100%;
        height: 100%;
        overflow: auto;
        background-color: rgba(0,0,0,0.4);
    }
    .modal-content {
        background-color: #fefefe;
        margin: 15% auto;
        padding: 20px;
        border: 1px solid #888;
        width: 80%;
        max-width: 400px;
        border-radius: 10px;
        text-align: center;
    }
    .modal-buttons {
        margin-top: 20px;
    }
    .modal-buttons button {
        margin: 0 10px;
        padding: 8px 16px;
        border-radius: 5px;
        border: none;
        cursor: pointer;
    }
    .modal-buttons .btn-yes {
        background-color: crimson;
        color: white;
    }
    .modal-buttons .btn-no {
        background-color: #ccc;
    }
</style>
</head>
<body>
<div class="container-fluid mt-3">
    <!-- 🔹 Chữ chạy -->
    <div class="marquee">
        <span>NHIỆT LIỆT CHÀO MỪNG ĐẠI HỘI ĐẢNG BỘ XÃ SƠN THỦY LẦN THỨ I, NHIỆM KỲ 2025-2030</span>
    </div>

    <!-- 🔹 Hiển thị ngày giờ hiện tại -->
    <div id="clock" class="clock"></div>

    <div class="mb-2 text-end text-muted small">
        ID của bạn: <span id="user-id">Đang tải...</span>
    </div>

    <ul class="nav nav-tabs" id="myTab" role="tablist">
        <li class="nav-item">
            <button class="nav-link active" data-bs-toggle="tab" data-bs-target="#quanly">📄 Quản lý Văn bản</button>
        </li>
        <li class="nav-item">
            <button class="nav-link" data-bs-toggle="tab" data-bs-target="#loc">🔍 Lọc & Tìm kiếm</button>
        </li>
    </ul>

    <div class="tab-content mt-3">
        <!-- TAB 1 -->
        <div class="tab-pane fade show active" id="quanly">
            <h2 class="text-center text-primary">QUẢN LÝ VĂN BẢN</h2>
            <div class="row g-3">
                <div class="col-md-3"><input type="text" id="kyhieu" class="form-control" placeholder="Ký hiệu văn bản"></div>
                <div class="col-md-3"><input type="text" id="noidung" class="form-control" placeholder="Nội dung văn bản"></div>
                <div class="col-md-3"><input type="text" id="lienket" class="form-control" placeholder="Liên kết văn bản"></div>
                <div class="col-md-3"><input type="text" id="timkiem" class="form-control" placeholder="🔍 Tìm kiếm ký hiệu" oninput="renderTable()"></div>
            </div>
            <button class="btn btn-success mt-3" onclick="themVanBan()">Thêm văn bản</button>
            <table class="table table-bordered mt-3">
                <thead>
                    <tr>
                        <th>STT</th>
                        <th>Ký hiệu VB</th>
                        <th>Nội dung</th>
                        <th>Xử lý VB</th>
                        <th>Liên kết</th>
                        <th>Thao tác</th>
                    </tr>
                </thead>
                <tbody id="doc-table"></tbody>
            </table>
        </div>
        <!-- TAB 2 -->
        <div class="tab-pane fade" id="loc">
            <h2 class="text-center text-primary">LỌC & THEO DÕI VĂN BẢN</h2>
            <div class="row g-3">
                <div class="col-md-4"><input type="text" id="searchKyHieu" class="form-control" placeholder="Tìm ký hiệu" oninput="renderLocTable()"></div>
                <div class="col-md-4"><input type="text" id="searchNoiDung" class="form-control" placeholder="Tìm nội dung" oninput="renderLocTable()"></div>
                <div class="col-md-4">
                    <select id="filterXuLy" class="form-select" onchange="renderLocTable()">
                        <option value="">-- Lọc theo trạng thái --</option>
                        <option value="Đã xử lý">Đã xử lý</option>
                        <option value="Chưa xử lý">Chưa xử lý</option>
                        <option value="Đang theo dõi">Đang theo dõi</option>
                        <option value="Đang xử lý">Đang xử lý</option>
                        <option value="Đã quá hạn">Đã quá hạn</option>
                    </select>
                </div>
            </div>
            <table class="table table-bordered mt-3">
                <thead>
                    <tr>
                        <th>STT</th>
                        <th>Ký hiệu VB</th>
                        <th>Nội dung</th>
                        <th>Xử lý VB</th>
                        <th>Liên kết</th>
                        <th>Thao tác</th>
                    </tr>
                </thead>
                <tbody id="doc-table-loc"></tbody>
            </table>
            <button class="btn btn-primary" onclick="xuatExcel()">📥 Xuất Excel</button>
            <div style="height:60px"></div>
        </div>
    </div>
</div>

<!-- Modal xác nhận tùy chỉnh -->
<div id="confirmModal" class="modal">
    <div class="modal-content">
        <p>Bạn có chắc chắn muốn xóa văn bản này?</p>
        <div class="modal-buttons">
            <button class="btn-yes" onclick="confirmAction(true)">Có</button>
            <button class="btn-no" onclick="confirmAction(false)">Không</button>
        </div>
    </div>
</div>

<!-- Thư viện -->
<script type="module">
    import { initializeApp } from "https://www.gstatic.com/firebasejs/11.6.1/firebase-app.js";
    import { getAuth, signInAnonymously, signInWithCustomToken, onAuthStateChanged } from "https://www.gstatic.com/firebasejs/11.6.1/firebase-auth.js";
    import { getFirestore, doc, getDoc, addDoc, setDoc, updateDoc, deleteDoc, onSnapshot, collection, query, where, getDocs } from "https://www.gstatic.com/firebasejs/11.6.1/firebase-firestore.js";
    
    // Global variables from Canvas
    const appId = typeof __app_id !== 'undefined' ? __app_id : 'default-app-id';
    const firebaseConfig = JSON.parse(typeof __firebase_config !== 'undefined' ? __firebase_config : '{}');
    const initialAuthToken = typeof __initial_auth_token !== 'undefined' ? __initial_auth_token : null;

    let db;
    let auth;
    let userId;
    let vanBanData = [];
    let vanBanRefs = {};

    window.onload = async () => {
        try {
            const app = initializeApp(firebaseConfig);
            db = getFirestore(app);
            auth = getAuth(app);

            // ✅ Khắc phục: Lắng nghe trạng thái đăng nhập, chỉ khi có user mới bắt đầu lắng nghe dữ liệu.
            onAuthStateChanged(auth, async (user) => {
                if (user) {
                    userId = user.uid;
                    document.getElementById('user-id').innerText = userId;
                    console.log("User signed in with UID:", userId);
                    setupRealtimeListener(); // Gọi sau khi userId đã được thiết lập
                } else {
                    console.log("No user signed in. Signing in anonymously...");
                    if (initialAuthToken) {
                        await signInWithCustomToken(auth, initialAuthToken);
                    } else {
                        await signInAnonymously(auth);
                    }
                }
            });
        } catch (error) {
            console.error("Error initializing Firebase or signing in:", error);
        }
    };
    
    function setupRealtimeListener() {
        const collectionPath = `/artifacts/${appId}/public/data/vanBanData`;
        console.log("Listening to collection:", collectionPath);
        const q = collection(db, collectionPath);
        
        onSnapshot(q, (querySnapshot) => {
            vanBanData = [];
            vanBanRefs = {};
            querySnapshot.forEach((doc) => {
                const docData = doc.data();
                vanBanData.push({ ...docData, docId: doc.id });
                vanBanRefs[docData.kyhieu] = doc.id;
            });
            vanBanData.sort((a, b) => new Date(a.ngayNhap) - new Date(b.ngayNhap));
            renderTable();
        }, (error) => {
            console.error("Error fetching data:", error);
        });
    }

    function getTrangThai(vb) {
        const now = new Date();
        const ngayNhap = new Date(vb.ngayNhap);
        const diffDays = Math.floor((now - ngayNhap) / (1000 * 60 * 60 * 24));

        if (vb.daXem) {
            if (diffDays <= 3) return "Đang xử lý";
            return "Đã xử lý";
        } else {
            if (diffDays < 3) return "Đang theo dõi";
            if (diffDays >= 3 && diffDays < 7) return "Chưa xử lý";
            if (diffDays >= 7) return "Đã quá hạn";
        }
        return "Đang theo dõi";
    }
    
    function renderTable() {
        const tbody = document.getElementById("doc-table");
        tbody.innerHTML = "";
        const keyword = document.getElementById("timkiem")?.value.toLowerCase() || "";
        
        let filtered = vanBanData.filter(vb => vb.kyhieu.toLowerCase().includes(keyword));

        filtered.forEach((vb, index) => {
            const trangThai = getTrangThai(vb);
            const isOwner = vb.userId && vb.userId === userId;
            
            // ✅ Khắc phục: Chỉ hiển thị nút xóa và cho phép chỉnh sửa nếu là chủ sở hữu
            let actionHtml = isOwner ?
                `<button class="delete-btn" onclick="showConfirmModal('${vb.kyhieu}')">Xóa</button>` :
                `Không thể xóa`;
            
            let contentEditable = isOwner ? 'true' : 'false';

            tbody.innerHTML += `<tr>
                <td>${index + 1}</td>
                <td>${vb.kyhieu}</td>
                <td contenteditable="${contentEditable}" onblur="capNhatNoiDung('${vb.kyhieu}', this.innerText)">${vb.noidung}</td>
                <td>${trangThai}</td>
                <td><a href="${vb.lienket}" target="_blank" onclick="danhDauDaXem('${vb.kyhieu}')">Xem</a></td>
                <td>${actionHtml}</td>
            </tr>`;
        });
        renderLocTable();
    }
    
    window.themVanBan = async function() {
        const kyhieu = document.getElementById("kyhieu").value.trim();
        const noidung = document.getElementById("noidung").value.trim();
        const lienket = document.getElementById("lienket").value.trim();
        if (!kyhieu || !noidung) {
            alert("Vui lòng nhập đầy đủ thông tin!");
            return;
        }
        const ngayNhap = new Date().toISOString();
        try {
            const docRef = await addDoc(collection(db, `/artifacts/${appId}/public/data/vanBanData`), {
                kyhieu,
                noidung,
                lienket,
                ngayNhap,
                daXem: false,
                userId: userId
            });
            console.log("Document written with ID: ", docRef.id);
            document.getElementById("kyhieu").value = "";
            document.getElementById("noidung").value = "";
            document.getElementById("lienket").value = "";
            alert("Văn bản đã được thêm thành công!");
        } catch (e) {
            console.error("Error adding document: ", e);
        }
    };
    
    window.capNhatNoiDung = async function(kyhieu, value) {
        const docData = vanBanData.find(vb => vb.kyhieu === kyhieu);
        if (docData && docData.userId === userId) {
            const docRef = doc(db, `/artifacts/${appId}/public/data/vanBanData`, docData.docId);
            await updateDoc(docRef, { noidung: value });
            console.log("Document updated successfully");
            alert("Nội dung đã được cập nhật thành công!");
        } else {
            console.warn("Unauthorized content update attempt.");
            alert("Bạn không có quyền chỉnh sửa văn bản này!");
        }
    };
    
    window.danhDauDaXem = async function(kyhieu) {
        const docData = vanBanData.find(vb => vb.kyhieu === kyhieu);
        if (docData) {
            const docRef = doc(db, `/artifacts/${appId}/public/data/vanBanData`, docData.docId);
            await updateDoc(docRef, { daXem: true });
        }
    };

    let vanBanToDelete = null;
    window.showConfirmModal = function(kyhieu) {
        const docData = vanBanData.find(vb => vb.kyhieu === kyhieu);
        if (docData && docData.userId === userId) {
            vanBanToDelete = docData;
            document.getElementById('confirmModal').style.display = 'block';
        } else {
            alert("Bạn không có quyền xóa văn bản này!");
        }
    };

    window.confirmAction = async function(isConfirmed) {
        document.getElementById('confirmModal').style.display = 'none';
        if (isConfirmed && vanBanToDelete) {
            const docId = vanBanToDelete.docId;
            try {
                // ✅ Khắc phục: Kiểm tra lại quyền xóa ở cấp độ chức năng
                if (vanBanToDelete.userId === userId) {
                    await deleteDoc(doc(db, `/artifacts/${appId}/public/data/vanBanData`, docId));
                    console.log("Document deleted successfully");
                    alert("Văn bản đã được xóa thành công!");
                } else {
                    console.warn("Unauthorized delete attempt.");
                    alert("Bạn không có quyền xóa văn bản này!");
                }
            } catch (e) {
                console.error("Error deleting document: ", e);
            }
        }
        vanBanToDelete = null;
    };

    window.renderLocTable = function() {
        const tbody = document.getElementById("doc-table-loc");
        tbody.innerHTML = "";
        const searchKyHieu = document.getElementById("searchKyHieu")?.value.toLowerCase() || "";
        const searchNoiDung = document.getElementById("searchNoiDung")?.value.toLowerCase() || "";
        const filterVal = document.getElementById("filterXuLy")?.value || "";

        let filtered = vanBanData.filter(vb => {
            const kyhieuOk = vb.kyhieu.toLowerCase().includes(searchKyHieu);
            const ndOk = vb.noidung.toLowerCase().includes(searchNoiDung);
            const tt = getTrangThai(vb);
            const filterOk = filterVal === "" || tt === filterVal;
            return kyhieuOk && ndOk && filterOk;
        });

        filtered.forEach((vb, index) => {
            const trangThai = getTrangThai(vb);
            const isOwner = vb.userId && vb.userId === userId;

            let actionHtml = isOwner ?
                `<button class="delete-btn" onclick="showConfirmModal('${vb.kyhieu}')">Xóa</button>` :
                `Không thể xóa`;

            let contentEditable = isOwner ? 'true' : 'false';

            tbody.innerHTML += `<tr>
                <td>${index + 1}</td>
                <td>${vb.kyhieu}</td>
                <td contenteditable="${contentEditable}" onblur="capNhatNoiDung('${vb.kyhieu}', this.innerText)">${vb.noidung}</td>
                <td>${trangThai}</td>
                <td><a href="${vb.lienket}" target="_blank" onclick="danhDauDaXem('${vb.kyhieu}')">Xem</a></td>
                <td class="no-print">${actionHtml}</td>
            </tr>`;
        });
    };
    
    window.xuatExcel = function() {
        const ws = XLSX.utils.json_to_sheet(vanBanData.map((vb, i) => ({
            STT: i + 1,
            "Ký hiệu VB": vb.kyhieu,
            "Nội dung": vb.noidung,
            "Xử lý VB": getTrangThai(vb),
            "Liên kết": vb.lienket
        })));
        const wb = XLSX.utils.book_new();
        XLSX.utils.book_append_sheet(wb, ws, "VanBan");
        XLSX.writeFile(wb, "VanBan_Xuat.xlsx");
    };

    function updateClock() {
        const now = new Date();
        const options = {
            weekday: 'long', year: 'numeric', month: '2-digit', day: '2-digit',
            hour: '2-digit', minute: '2-digit', second: '2-digit'
        };
        const clockEl = document.getElementById('clock');
        if (clockEl) {
            clockEl.innerText = now.toLocaleDateString('vi-VN', options);
        }
    }
    setInterval(updateClock, 1000);
    updateClock();
</script>

<script src="https://cdnjs.cloudflare.com/ajax/libs/xlsx/0.18.5/xlsx.full.min.js"></script>
<script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.3/dist/js/bootstrap.bundle.min.js"></script>

<!-- 🔹 Footer -->
<button id="backToTopBtn">⬆ Về đầu trang</button>
<script>
    const btn = document.getElementById("backToTopBtn");
    window.addEventListener("scroll", () => {
        if (document.documentElement.scrollTop > 200) {
            btn.style.display = "block";
        } else {
            btn.style.display = "none";
        }
    });
    btn.addEventListener("click", () => {
        window.scrollTo({ top: 0, behavior: "smooth" });
    });
</script>
<footer class="footer">
    <p>© 2025 Bản quyền thuộc về: <strong>QB</strong></p>
    <p></p>
    <nav>
        <a href="help.html">Hướng dẫn sử dụng</a>
    </nav>
</footer>
</body>
</html>
