Tổng hợp các mẫu Response API trong dự án QLDT

1. API Lịch sử giao dịch (transactionHistoryService)
   1.1. Lấy danh sách giao dịch
   // GET /api/transaction-history
   {
   id: "1",
   transactionId: "PAY20240515001",
   date: "2024-05-15T10:30:45",
   type: "tuition", // "tuition" | "deposit" | "fee" | "refund"
   description: "Thanh toán học phí học kỳ 2, năm học 2023-2024",
   amount: 8500000,
   paymentMethod: "Thẻ ATM",
   status: "success", // "success" | "pending" | "failed"
   details: {
   cardInfo: "\***\* \*\*** \*\*\*\* 5678",
   bank: "Vietcombank",
   partnerTransactionId: "VNPAY123456789",
   note: "Thanh toán học phí học kỳ 2 năm học 2023-2024",
   user: "Nguyễn Văn A",
   }
   }
   1.2. Lấy thống kê giao dịch
   // GET /api/transaction-history/stats
   {
   totalCount: 10,
   totalAmount: 50000000,
   monthlyCount: 2,
   monthlyAmount: 15000000
   }
   1.3. Lấy dữ liệu biểu đồ
   // GET /api/transaction-history/chart-data
   {
   byType: [
   {
   type: "Học phí",
   count: 4,
   percentage: 40,
   color: "#4caf50"
   },
   {
   type: "Nạp tiền",
   count: 2,
   percentage: 20,
   color: "#2196f3"
   },
   {
   type: "Các khoản thu khác",
   count: 3,
   percentage: 30,
   color: "#ff9800"
   },
   {
   type: "Hoàn tiền",
   count: 1,
   percentage: 10,
   color: "#9c27b0"
   }
   ]
   }
   1.4. Tải biên lai giao dịch
   // GET /api/transaction-history/receipt/{transactionId}
   {
   success: true,
   fileUrl: "/receipts/PAY20240515001.pdf"
   }
2. API Học phí (tuitionService)
   2.1. Lấy thống kê học phí
   // GET /api/tuition/summary
   {
   totalTuition: 15000000,
   totalPaid: 15000000,
   totalDebt: 0,
   totalExcess: 0
   }
   2.2. Lấy danh sách học phí
   // GET /api/tuition/items
   [
   {
   id: "tuition1",
   semester: "Học kỳ 1",
   academicYear: "2020-2021",
   semesterCode: "2020-2021-1",
   description: "Học phí học kỳ 1",
   amount: 8500000,
   paid: 8500000,
   dueDate: "2020-09-15",
   status: "paid", // "paid" | "pending" | "overdue"
   registeredCredits: 20
   }
   ]
   2.3. Lấy chi tiết học phí
   // GET /api/tuition/detail/{semesterCode}
   {
   tuitionItem: {
   id: "tuition8",
   semester: "Học kỳ 2",
   academicYear: "2023-2024",
   semesterCode: "2023-2024-2",
   description: "Học phí học kỳ 2",
   amount: 15000000,
   paid: 15000000,
   dueDate: "2024-01-15",
   status: "paid",
   registeredCredits: 24
   },
   courses: [
   {
   id: "course1",
   code: "LTWNC01",
   name: "Lập trình Web nâng cao",
   credits: 3,
   pricePerCredit: 625000,
   totalPrice: 1875000
   }
   ]
   }
   2.4. Lấy lịch sử thanh toán
   // GET /api/tuition/payments?semester={semesterCode}
   [
   {
   id: "payment1",
   date: "2024-02-10",
   amount: 15000000,
   method: "Chuyển khoản ngân hàng",
   transactionId: "VNPAY123456789",
   status: "completed" // "completed" | "pending" | "failed"
   }
   ]
3. API Kết quả học tập (academicResultsService)
   3.1. Lấy thông tin chung
   // GET /api/academic-results/info
   {
   studentId: "20020001",
   studentName: "Nguyễn Văn A",
   major: "Công nghệ thông tin",
   class: "CNTT2020",
   currentSemester: "Học kỳ 2, năm học 2023-2024",
   gpa: 3.65,
   totalCredits: 140,
   completedCredits: 110,
   academicRank: "Giỏi",
   disciplineScore: 85,
   maxDisciplineScore: 100
   }
   3.2. Lấy danh sách học kỳ
   // GET /api/academic-results/semesters
   [
   {
   id: "all",
   name: "Tất cả các học kỳ",
   isCurrent: false
   },
   {
   id: "2023-2024-1",
   name: "Học kỳ 1, năm học 2023-2024",
   isCurrent: true
   }
   ]
   3.3. Lấy kết quả học tập
   // GET /api/academic-results/courses?semesterId={semesterId}&courseType={courseType}
   [
   {
   id: "course1",
   courseCode: "CNPM01",
   courseName: "Công nghệ phần mềm",
   credits: 3,
   semester: "Học kỳ 1, năm học 2023-2024",
   semesterId: "2023-2024-1",
   attendance: 10,
   assignment: 9,
   practice: 8,
   midterm: 8.5,
   final: 8,
   total: 8.4,
   letterGrade: "A",
   gradePoint: 4.0,
   status: "passed", // "passed" | "failed" | "inprogress"
   courseType: "specialized" // "all" | "required" | "elective" | "general" | "specialized"
   }
   ]
   3.4. Lấy phân bố điểm
   // GET /api/academic-results/grade-distribution?semesterId={semesterId}
   [
   {
   grade: "A/A+",
   percentage: 40,
   color: "linear-gradient(to right, #4caf50, #81c784)"
   },
   {
   grade: "B+",
   percentage: 30,
   color: "linear-gradient(to right, #2196f3, #64b5f6)"
   }
   ]
   3.5. Lấy tiến độ học tập
   // GET /api/academic-results/progress
   {
   totalCredits: 140,
   completedCredits: 110,
   remainingCredits: 30,
   currentCredits: 24,
   completionPercentage: 78.6,
   categories: [
   {
   id: "general",
   name: "Khối kiến thức đại cương",
   icon: "fa-book",
   totalCredits: 35,
   completedCredits: 35,
   completionPercentage: 100
   }
   ]
   }
4. API Thông tin sinh viên (studentProfileService)
   4.1. Lấy hồ sơ sinh viên
   // GET /api/student/profile
   {
   id: "1",
   studentId: "SV12345",
   avatar: "/images/chup-chan-dung-5.jpg",
   className: "CNTT2020",
   status: "Đang học",
   personalInfo: {
   fullName: "Nguyễn Văn A",
   dateOfBirth: "2002-05-15",
   gender: "Nam",
   idNumber: "0123456789",
   idIssueDate: "2019-06-10",
   idIssuePlace: "Công an tỉnh Đồng Nai",
   ethnicity: "Kinh",
   religion: "Không",
   nationality: "Việt Nam",
   priorityObject: "Không",
   area: "2NT",
   isYouthUnionMember: true,
   isPartyMember: false,
   youthUnionJoinDate: "2017-03-26",
   youthUnionJoinPlace: "Trường THPT Nguyễn Hữu Cảnh"
   },
   academicInfo: {
   faculty: "Công nghệ thông tin",
   major: "Công nghệ thông tin",
   specialization: "Công nghệ phần mềm",
   className: "CNTT2020",
   course: "2020-2024",
   educationLevel: "Đại học",
   educationType: "Chính quy",
   academicAdvisor: "TS. Nguyễn Văn X",
   highSchool: "THPT Nguyễn Hữu Cảnh",
   highSchoolGraduationYear: "2020",
   nationalExamScore: 24.5,
   admissionCombination: "A00 (Toán, Lý, Hóa)",
   admissionMethod: "Xét điểm thi THPT QG",
   gpa: 3.65,
   academicStanding: "Giỏi",
   registeredCredits: 120,
   completedCredits: 110,
   remainingCredits: 30,
   conductScore: 85,
   conductRating: "Tốt"
   },
   contactInfo: {
   phone: "0987654321",
   personalEmail: "nguyenvana@gmail.com",
   schoolEmail: "sv12345@dntu.edu.vn",
   facebook: "facebook.com/nguyenvana",
   permanentAddress: "123 Đường A, Phường B, TP. Biên Hòa, Đồng Nai",
   temporaryAddress: "456 Đường C, Phường D, TP. Biên Hòa, Đồng Nai",
   currentResidence: "Ký túc xá trường, Phòng B205",
   emergencyContact: {
   name: "Nguyễn Văn B",
   relationship: "Bố",
   phone: "0912345678",
   address: "123 Đường A, Phường B, TP. Biên Hòa, Đồng Nai"
   }
   },
   familyInfo: {
   father: {
   name: "Nguyễn Văn B",
   birthYear: "1975",
   occupation: "Kỹ sư xây dựng",
   workplace: "Công ty Xây dựng ABC",
   phone: "0912345678"
   },
   mother: {
   name: "Trần Thị C",
   birthYear: "1978",
   occupation: "Giáo viên",
   workplace: "Trường THCS XYZ",
   phone: "0923456789"
   },
   siblings: [
   {
   name: "Nguyễn Thị D",
   birthYear: "2005",
   relationship: "Em gái",
   occupation: "Học sinh",
   workplace: "",
   studyPlace: "Trường THPT Nguyễn Hữu Cảnh",
   phone: ""
   }
   ]
   },
   documents: [
   {
   id: "doc1",
   name: "Căn cước công dân",
   status: "completed", // "completed" | "processing" | "not-submitted"
   fileUrl: "/documents/cccd.pdf",
   icon: "fa-id-card"
   }
   ],
   tuition: [
   {
   id: "tuition1",
   semester: "Học kỳ 1",
   academicYear: "2020-2021",
   description: "Học phí học kỳ 1",
   amount: 8500000,
   paid: 8500000,
   dueDate: "2020-09-15"
   }
   ]
   }
5. API Lịch thi (examScheduleService)
   5.1. Lấy thông tin chung
   // GET /api/exam-schedule/info
   {
   studentId: "20020001",
   studentName: "Nguyễn Văn A",
   major: "Công nghệ thông tin",
   class: "CNTT2020",
   currentSemester: "Học kỳ 2, năm học 2023-2024"
   }
   5.2. Lấy danh sách học kỳ
   // GET /api/exam-schedule/semesters
   [
   {
   id: "2023-2024-2",
   name: "Học kỳ 2, năm học 2023-2024",
   isCurrent: true
   },
   {
   id: "2023-2024-1",
   name: "Học kỳ 1, năm học 2023-2024",
   isCurrent: false
   }
   ]
   5.3. Lấy thông báo lịch thi
   // GET /api/exam-schedule/notifications?semesterId={semesterId}
   [
   {
   id: "notification1",
   title: "Thông báo về kỳ thi cuối kỳ học kỳ 2 năm học 2023-2024",
   date: "01/06/2024",
   author: "Phòng Đào tạo",
   content: "Kỳ thi cuối kỳ sẽ diễn ra từ ngày 15/06/2024 đến ngày 30/06/2024...",
   isImportant: true
   }
   ]
   5.4. Lấy thống kê lịch thi
   // GET /api/exam-schedule/stats?semesterId={semesterId}
   {
   totalExams: 8,
   daysUntilExam: 14,
   completedExams: 0,
   remainingExams: 8,
   examRooms: ["A305", "A401", "B203"],
   lastUpdated: "01/06/2024",
   nextExamDate: "15/06/2024",
   examType: "Kỳ thi cuối kỳ"
   }
   5.5. Lấy lịch thi
   // GET /api/exam-schedule/schedules?semesterId={semesterId}&examType={examType}
   [
   {
   id: "exam1",
   courseCode: "LTWNC01",
   courseName: "Lập trình Web nâng cao",
   examDate: "15/06/2024",
   startTime: "07:00",
   endTime: "08:30",
   room: "A305",
   className: "CNTT2020",
   examType: "final", // "all" | "midterm" | "final" | "makeup"
   examFormat: "Thi viết",
   notes: "Mang theo bút, thước kẻ",
   status: "upcoming", // "upcoming" | "completed" | "cancelled"
   dayOfWeek: 7 // 2-8 (Thứ 2 đến Chủ nhật)
   }
   ]
   5.6. Lấy quy định thi
   // GET /api/exam-schedule/regulations
   [
   {
   id: "reg1",
   title: "Thời gian",
   icon: "fa-clock-o",
   content: "Sinh viên phải có mặt tại phòng thi trước giờ thi ít nhất 15 phút..."
   }
   ]
   Đây là tổng hợp các mẫu response API chính trong dự án QLDT. Mỗi API đều có cấu trúc dữ liệu rõ ràng và được định nghĩa bằng TypeScript interface, giúp cho việc phát triển frontend dễ dàng hơn.
