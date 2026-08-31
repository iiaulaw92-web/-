import React, { useState } from 'react';
import { 
  LayoutDashboard, 
  Scale, 
  ShoppingCart, 
  Video, 
  Users, 
  FileText, 
  Calendar, 
  Upload, 
  Send, 
  Search,
  Gavel,
  Calculator
} from 'lucide-react';

// --- کامپوننت‌های داخلی (برای سادگی همه در یک فایل) ---

// 1. صفحه داشبورد
const Dashboard = () => (
  <div className="space-y-6">
    <h2 className="text-2xl font-bold text-slate-800">داشبورد مدیریت</h2>
    <div className="grid grid-cols-1 md:grid-cols-3 gap-6">
      <div className="bg-white p-6 rounded-xl shadow-sm border-r-4 border-blue-500">
        <h3 className="text-gray-500 text-sm">پرونده‌های فعال</h3>
        <p className="text-3xl font-bold mt-2">۱۲</p>
      </div>
      <div className="bg-white p-6 rounded-xl shadow-sm border-r-4 border-green-500">
        <h3 className="text-gray-500 text-sm">درآمد ماه جاری</h3>
        <p className="text-3xl font-bold mt-2">۴۵,۰۰۰,۰۰۰ تومان</p>
      </div>
      <div className="bg-white p-6 rounded-xl shadow-sm border-r-4 border-yellow-500">
        <h3 className="text-gray-500 text-sm">جلسات آینده</h3>
        <p className="text-3xl font-bold mt-2">۳ جلسه</p>
      </div>
    </div>
    
    {/* تقویم شمسی ساده */}
    <div className="bg-white p-6 rounded-xl shadow-sm">
      <h3 className="font-bold mb-4 flex items-center gap-2"><Calendar size={20} /> تقویم کاری (شمسی)</h3>
      <div className="grid grid-cols-7 gap-2 text-center text-sm">
        {['ش', 'ی', 'د', 'س', 'چ', 'پ', 'ج'].map(d => <div key={d} className="font-bold text-blue-600">{d}</div>)}
        {Array.from({length: 30}, (_, i) => (
          <div key={i} className={`p-2 rounded hover:bg-blue-50 cursor-pointer ${i === 14 ? 'bg-blue-600 text-white' : ''}`}>
            {i + 1}
          </div>
        ))}
      </div>
    </div>
  </div>
);

// 2. مدیریت پرونده و تبادل اسناد
const CaseManager = () => {
  const [messages, setMessages] = useState([
    { id: 1, sender: 'client', text: 'سلام آقای وکیل، عکس سند ملک را فرستادم.', time: '10:30' },
    { id: 2, sender: 'lawyer', text: 'دریافت شد. لطفاً اصل مدارک را نیز اسکن کنید.', time: '10:35' }
  ]);
  const [newMessage, setNewMessage] = useState('');

  const handleSend = () => {
    if (newMessage.trim()) {
      setMessages([...messages, { id: Date.now(), sender: 'lawyer', text: newMessage, time: 'Now' }]);
      setNewMessage('');
    }
  };

  return (
    <div className="bg-white rounded-xl shadow-lg h-[80vh] flex flex-col overflow-hidden">
      <div className="p-4 border-b bg-slate-50 flex justify-between items-center">
        <h2 className="font-bold text-lg">پرونده شماره ۱۴۰۲/۵۶ - آقای محمدی</h2>
        <span className="bg-green-100 text-green-800 text-xs px-2 py-1 rounded">در جریان رسیدگی</span>
      </div>
      
      <div className="flex-1 overflow-y-auto p-4 space-y-4 bg-gray-50">
        {messages.map((msg) => (
          <div key={msg.id} className={`flex ${msg.sender === 'lawyer' ? 'justify-start' : 'justify-end'}`}>
            <div className={`max-w-[70%] p-3 rounded-lg text-sm ${msg.sender === 'lawyer' ? 'bg-white border shadow-sm' : 'bg-blue-600 text-white'}`}>
              <p>{msg.text}</p>
              <span className="text-xs opacity-70 block mt-1 text-left">{msg.time}</span>
            </div>
          </div>
        ))}
      </div>

      <div className="p-4 border-t bg-white flex gap-2">
        <button className="p-2 text-gray-500 hover:bg-gray-100 rounded"><Upload size={20} /></button>
        <input 
          type="text" 
          value={newMessage}
          onChange={(e) => setNewMessage(e.target.value)}
          placeholder="پیام خود را بنویسید..." 
          className="flex-1 border rounded-lg px-4 py-2 focus:outline-none focus:border-blue-500"
          onKeyPress={(e) => e.key === 'Enter' && handleSend()}
        />
        <button onClick={handleSend} className="p-2 bg-blue-600 text-white rounded-lg hover:bg-blue-700"><Send size={20} /></button>
      </div>
    </div>
  );
};

// 3. فروشگاه لوایح و خدمات
const Marketplace = () => {
  const products = [
    { id: 1, title: 'دادخواست مطالبه وجه چک', price: '۱۵۰,۰۰۰', type: 'PDF' },
    { id: 2, title: 'لایحه دفاعیه کیفری (سرقت)', price: '۲۰۰,۰۰۰', type: 'Word' },
    { id: 3, title: 'قرارداد مشارکت مدنی', price: '۳۵۰,۰۰۰', type: 'PDF' },
    { id: 4, title: 'شکواییه توهین و افترا', price: '۱۰۰,۰۰۰', type: 'Word' },
  ];

  return (
    <div>
      <h2 className="text-2xl font-bold mb-6">فروشگاه خدمات و لوایح حقوقی</h2>
      <div className="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-6">
        {products.map(p => (
          <div key={p.id} className="bg-white p-4 rounded-xl shadow-sm hover:shadow-md transition border">
            <div className="h-32 bg-slate-100 rounded-lg mb-4 flex items-center justify-center text-slate-400">
              <FileText size={40} />
            </div>
            <h3 className="font-bold text-sm mb-2">{p.title}</h3>
            <div className="flex justify-between items-center mt-4">
              <span className="text-blue-600 font-bold">{p.price} تومان</span>
              <button className="bg-slate-900 text-white text-xs px-3 py-1.5 rounded hover:bg-slate-700">خرید</button>
            </div>
          </div>
        ))}
      </div>
    </div>
  );
};

// 4. ابزارهای حقوقی (محاسبه‌گر)
const LegalTools = () => {
  const [amount, setAmount] = useState('');
  const [result, setResult] = useState(null);

  const calculateCost = () => {
    // فرمول ساده شده هزینه دادرسی (مثال)
    const val = parseFloat(amount.replace(/,/g, ''));
    if (!val) return;
    const cost = val * 0.035; // 3.5 درصد
    setResult(cost.toLocaleString());
  };

  return (
    <div className="max-w-2xl mx-auto">
      <h2 className="text-2xl font-bold mb-6 flex items-center gap-2"><Calculator /> محاسبه‌گر هزینه دادرسی</h2>
      <div className="bg-white p-8 rounded-xl shadow-lg">
        <label className="block text-sm font-medium text-gray-700 mb-2">مبلغ خواسته (تومان)</label>
        <input 
          type="text" 
          value={amount}
          onChange={(e) => setAmount(e.target.value)}
          className="w-full border rounded-lg px-4 py-3 mb-4 text-left dir-ltr"
          placeholder="مثلا: 10000000"
        />
        <button 
          onClick={calculateCost}
          className="w-full bg-blue-600 text-white py-3 rounded-lg font-bold hover:bg-blue-700 transition"
        >
          محاسبه کن
        </button>
        
        {result && (
          <div className="mt-6 p-4 bg-green-50 border border-green-200 rounded-lg text-center">
            <p className="text-gray-600 text-sm">هزینه تقریبی دادرسی:</p>
            <p className="text-2xl font-bold text-green-700 mt-1">{result} تومان</p>
          </div>
        )}
      </div>
    </div>
  );
};

// --- کامپوننت اصلی برنامه ---
export default function App() {
  const [activeTab, setActiveTab] = useState('dashboard');

  const renderContent = () => {
    switch(activeTab) {
      case 'dashboard': return <Dashboard />;
      case 'cases': return <CaseManager />;
      case 'market': return <Marketplace />;
      case 'tools': return <LegalTools />;
      default: return <Dashboard />;
    }
  };

  const NavItem = ({ id, icon: Icon, label }) => (
    <button 
      onClick={() => setActiveTab(id)}
      className={`w-full flex items-center gap-3 p-3 rounded-lg transition ${activeTab === id ? 'bg-blue-600 text-white shadow-lg' : 'text-slate-400 hover:bg-slate-800 hover:text-white'}`}
    >
      <Icon size={20} />
      <span className="font-medium">{label}</span>
    </button>
  );

  return (
    <div className="flex min-h-screen bg-gray-100 font-sans" dir="rtl">
      {/* سایدبار */}
      <aside className="w-72 bg-slate-900 text-white p-6 fixed h-full right-0 top-0 shadow-2xl z-10">
        <div className="flex items-center gap-3 mb-10 px-2">
          <div className="bg-yellow-500 p-2 rounded-lg">
            <Gavel className="text-slate-900" size={24} />
          </div>
          <h1 className="text-2xl font-bold tracking-tight">حق‌گستر</h1>
        </div>
        
        <nav className="space-y-2">
          <NavItem id="dashboard" icon={LayoutDashboard} label="داشبورد اصلی" />
          <NavItem id="cases" icon={FileText} label="مدیریت پرونده‌ها" />
          <NavItem id="market" icon={ShoppingCart} label="فروشگاه لوایح" />
          <NavItem id="tools" icon={Scale} label="ابزارهای حقوقی" />
          <div className="my-6 border-t border-slate-700"></div>
          <NavItem id="users" icon={Users} label="موکلین و وکلا" />
          <NavItem id="media" icon={Video} label="ویدیوهای آموزشی" />
        </nav>

        <div className="absolute bottom-6 right-6 left-6">
          <div className="bg-slate-800 p-4 rounded-xl flex items-center gap-3">
            <div className="w-10 h-10 bg-blue-500 rounded-full flex items-center justify-center font-bold">آ</div>
            <div>
              <p className="text-sm font-bold">افشین سوری</p>
              <p className="text-xs text-slate-400">وکیل پایه یک</p>
            </div>
          </div>
        </div>
      </aside>

      {/* محتوای اصلی */}
      <main className="flex-1 mr-72 p-8 overflow-y-auto h-screen">
        {/* هدر بالا */}
        <header className="flex justify-between items-center mb-8">
          <div className="relative w-96">
            <Search className="absolute right-3 top-3 text-gray-400" size={20} />
            <input 
              type="text" 
              placeholder="جستجو در پرونده‌ها، قوانین یا لوایح..." 
              className="w-full bg-white border-none rounded-xl py-3 pr-10 pl-4 shadow-sm focus:ring-2 focus:ring-blue-500 outline-none"
            />
          </div>
          <div className="flex gap-4">
            <button className="bg-white p-3 rounded-xl shadow-sm text-gray-600 hover:text-blue-600 relative">
              <span className="absolute top-2 left-2 w-2 h-2 bg-red-500 rounded-full"></span>
              <Scale size={20} />
            </button>
          </div>
        </header>

        {renderContent()}
      </main>
    </div>
  );
}
