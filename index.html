import React, { useState, useEffect, useMemo } from 'react';
import {
  Plane, Calendar, CreditCard, Wallet, Plus, Trash2, Edit3, ArrowRightLeft,
  PieChart, Users, DollarSign, Sparkles, Filter, Search, ChevronRight,
  TrendingUp, Download, RefreshCw, CheckCircle, ShieldCheck, MapPin, 
  Coffee, Utensils, Ticket, Shirt, Bus, MoreHorizontal, Home, Info, ArrowUpRight,
  Copy, Check, UserPlus, AlertCircle
} from 'lucide-react';

// --- 星展銀行 (DBS) 專屬預設卡庫 ---
const DBS_INITIAL_CARDS = [
  { 
    id: 'dbs-eco', 
    name: '星展 eco 永續卡 (日韓歐美加碼)', 
    rate: 5.0, 
    fee: 1.5, 
    notes: '日/韓/歐美/新加坡實體加碼最優 5%，扣除 1.5% 海外手續費淨賺 3.5%' 
  },
  { 
    id: 'dbs-eco-general', 
    name: '星展 eco 永續卡 (一般海外/網購)', 
    rate: 1.5, 
    fee: 1.5, 
    notes: '國內外基礎消費 1.5% 現金積點無上限，剛好抵銷 1.5% 海外手續費' 
  },
  { 
    id: 'dbs-flight', 
    name: '星展 飛行世界卡 (哩程累積)', 
    rate: 3.3, 
    fee: 1.5, 
    notes: '海外每 NT$15 = 1 哩 (約 3.3% 價值)，長榮/華航/亞洲萬里通自由兌換' 
  },
  { 
    id: 'dbs-everyday', 
    name: '星展 everyday 威士御璽卡', 
    rate: 3.0, 
    fee: 1.5, 
    notes: '指定日常消費與海外享活利積分加倍折抵' 
  },
  { 
    id: 'dbs-custom', 
    name: '自訂其他星展信用卡', 
    rate: 2.0, 
    fee: 1.5, 
    notes: '可自由調整回饋率與手續費' 
  }
];

// --- 全新乾淨初始狀態：僅保留基礎範本架構，無任何示範消費與換匯紀錄 ---
const CLEAN_INITIAL_TRIPS = [
  {
    id: 'trip-my-first-trip',
    name: '我的第一趟旅程 (點擊可切換或新增)',
    startDate: new Date().toISOString().split('T')[0],
    endDate: new Date(Date.now() + 6 * 24 * 60 * 60 * 1000).toISOString().split('T')[0],
    currency: 'JPY',
    currencySymbol: '¥',
    targetBudgetTWD: 50000,
    companions: ['我', '旅伴A'],
    exchanges: [],
    expenses: []
  }
];

const CATEGORY_CONFIG = {
  機票: { icon: Plane, bg: 'bg-sky-50 text-sky-600', border: 'border-sky-200', bar: 'from-sky-500 to-blue-500' },
  住宿: { icon: Home, bg: 'bg-indigo-50 text-indigo-600', border: 'border-indigo-200', bar: 'from-indigo-500 to-blue-600' },
  食: { icon: Utensils, bg: 'bg-amber-50 text-amber-600', border: 'border-amber-200', bar: 'from-amber-400 to-orange-500' },
  喝: { icon: Coffee, bg: 'bg-orange-50 text-orange-600', border: 'border-orange-200', bar: 'from-orange-400 to-rose-400' },
  娛樂: { icon: Ticket, bg: 'bg-purple-50 text-purple-600', border: 'border-purple-200', bar: 'from-purple-500 to-indigo-500' },
  衣服: { icon: Shirt, bg: 'bg-pink-50 text-pink-600', border: 'border-pink-200', bar: 'from-pink-400 to-rose-400' },
  交通: { icon: Bus, bg: 'bg-teal-50 text-teal-600', border: 'border-teal-200', bar: 'from-teal-400 to-cyan-500' },
  其他: { icon: MoreHorizontal, bg: 'bg-slate-100 text-slate-600', border: 'border-slate-200', bar: 'from-slate-400 to-slate-500' },
};

export default function TravelBudgetApp() {
  // --- 狀態維護 (localStorage) ---
  const [trips, setTrips] = useState(() => {
    const saved = localStorage.getItem('DBS_TRAVEL_TRIPS_V3_CLEAN');
    return saved ? JSON.parse(saved) : CLEAN_INITIAL_TRIPS;
  });

  const [cards, setCards] = useState(() => {
    const saved = localStorage.getItem('DBS_CARDS_DATA_V3');
    return saved ? JSON.parse(saved) : DBS_INITIAL_CARDS;
  });

  const [activeTripId, setActiveTripId] = useState(() => trips[0]?.id || '');
  const [activeTab, setActiveTab] = useState('expenses'); // 'expenses' | 'analytics' | 'exchange' | 'cards' | 'split'
  const [copiedSuccess, setCopiedSuccess] = useState(false);

  useEffect(() => {
    localStorage.setItem('DBS_TRAVEL_TRIPS_V3_CLEAN', JSON.stringify(trips));
  }, [trips]);

  useEffect(() => {
    localStorage.setItem('DBS_CARDS_DATA_V3', JSON.stringify(cards));
  }, [cards]);

  // 當前選取之旅程
  const currentTrip = useMemo(() => {
    return trips.find((t) => t.id === activeTripId) || trips[0] || null;
  }, [trips, activeTripId]);

  // --- 換匯加權平均計算 ---
  const exchangeStats = useMemo(() => {
    if (!currentTrip || !currentTrip.exchanges || currentTrip.exchanges.length === 0) {
      return { totalTwd: 0, totalForeign: 0, avgRate: 0.22 };
    }
    const totalTwd = currentTrip.exchanges.reduce((sum, item) => sum + Number(item.twdAmount || 0), 0);
    const totalForeign = currentTrip.exchanges.reduce((sum, item) => sum + Number(item.foreignAmount || 0), 0);
    const avgRate = totalForeign > 0 ? totalTwd / totalForeign : 0.22;
    return { totalTwd, totalForeign, avgRate };
  }, [currentTrip]);

  // --- 換算為台幣的輔助函數 ---
  const convertToTWD = (item) => {
    if (!item) return 0;
    if (item.currency === 'TWD') {
      return Number(item.origAmount || 0);
    }
    const rate = exchangeStats.avgRate || 0.22;
    return Math.round(Number(item.origAmount || 0) * rate);
  };

  // --- 星展信用卡回饋與手續費計算 (1.5%手續費) ---
  const calculateCardRewards = (item) => {
    if (item.payMethod !== 'card' || !item.cardId) {
      return { feeTWD: 0, rewardTWD: 0, netRewardTWD: 0, cardName: '' };
    }
    const card = cards.find((c) => c.id === item.cardId);
    if (!card) return { feeTWD: 0, rewardTWD: 0, netRewardTWD: 0, cardName: '星展卡' };

    const twdVal = convertToTWD(item);
    const feeTWD = Math.round(twdVal * (Number(card.fee || 1.5) / 100));
    const rewardTWD = Math.round(twdVal * (Number(card.rate || 0) / 100));
    const netRewardTWD = rewardTWD - feeTWD;

    return {
      feeTWD,
      rewardTWD,
      netRewardTWD,
      cardName: card.name,
      rate: card.rate,
      fee: card.fee
    };
  };

  // --- 核心運算：計算各旅伴的代墊與負擔明細 ---
  const memberBalances = useMemo(() => {
    if (!currentTrip || !currentTrip.companions) return { balances: {}, myTotalShare: 0 };

    const companions = currentTrip.companions;
    // paid: 先代墊總額, owed: 享受花費應負擔總額
    const balanceMap = {};
    companions.forEach(c => {
      balanceMap[c] = { paid: 0, owed: 0, net: 0 };
    });

    currentTrip.expenses.forEach(item => {
      const twd = convertToTWD(item);
      const payer = item.payer || '我';
      if (!balanceMap[payer]) balanceMap[payer] = { paid: 0, owed: 0, net: 0 };

      // 1. 付款人先墊付了此筆全額
      balanceMap[payer].paid += twd;

      // 2. 依分攤方式計算誰應該負擔多少
      if (item.splitType === 'self') {
        // 全額自費（僅付款人自己負擔）
        balanceMap[payer].owed += twd;
      } 
      else if (item.splitType === 'selected_even') {
        // 多選成員平分 (例如4人旅程，只有勾選的2人或3人分)
        const participants = (item.involvedCompanions && item.involvedCompanions.length > 0)
          ? item.involvedCompanions
          : [payer];
        const count = participants.length;
        const perPerson = Math.floor(twd / count);
        let remainder = twd - (perPerson * count);

        participants.forEach((p, idx) => {
          if (!balanceMap[p]) balanceMap[p] = { paid: 0, owed: 0, net: 0 };
          const share = perPerson + (idx === 0 ? remainder : 0);
          balanceMap[p].owed += share;
        });
      } 
      else if (item.splitType === 'custom_amount') {
        // 自訂每人各自付多少
        const customAmounts = item.customAmounts || {};
        Object.entries(customAmounts).forEach(([person, amt]) => {
          if (!balanceMap[person]) balanceMap[person] = { paid: 0, owed: 0, net: 0 };
          // 換算成台幣比重
          let personTwd = 0;
          if (item.currency === 'TWD') {
            personTwd = Number(amt || 0);
          } else {
            personTwd = Math.round(Number(amt || 0) * (exchangeStats.avgRate || 0.22));
          }
          balanceMap[person].owed += personTwd;
        });
      } 
      else if (item.splitType === 'single_reimburse') {
        // 專為特定單人全額代墊
        const target = item.targetCompanion || payer;
        if (!balanceMap[target]) balanceMap[target] = { paid: 0, owed: 0, net: 0 };
        balanceMap[target].owed += twd;
      }
    });

    // 結算 net = paid - owed (正數為應收回，負數為應給付)
    Object.keys(balanceMap).forEach(p => {
      balanceMap[p].net = balanceMap[p].paid - balanceMap[p].owed;
    });

    return {
      balances: balanceMap,
      myTotalShare: balanceMap['我'] ? balanceMap['我'].owed : 0
    };
  }, [currentTrip, exchangeStats]);

  // --- 最佳化簡化轉帳算式 (誰給誰多少錢) ---
  const settlementTransfers = useMemo(() => {
    if (!memberBalances || !memberBalances.balances) return [];

    // 分為債權人(net > 0)與債務人(net < 0)
    let creditors = [];
    let debtors = [];

    Object.entries(memberBalances.balances).forEach(([name, data]) => {
      if (data.net > 1) {
        creditors.push({ name, amount: data.net });
      } else if (data.net < -1) {
        debtors.push({ name, amount: Math.abs(data.net) });
      }
    });

    // 排序由大至小加速匹配
    creditors.sort((a, b) => b.amount - a.amount);
    debtors.sort((a, b) => b.amount - a.amount);

    const transfers = [];
    let i = 0; // debtors
    let j = 0; // creditors

    while (i < debtors.length && j < creditors.length) {
      const debtor = debtors[i];
      const creditor = creditors[j];
      const settleAmount = Math.min(debtor.amount, creditor.amount);

      if (settleAmount > 0) {
        transfers.push({
          from: debtor.name,
          to: creditor.name,
          amount: Math.round(settleAmount)
        });
      }

      debtor.amount -= settleAmount;
      creditor.amount -= settleAmount;

      if (debtor.amount <= 1) i++;
      if (creditor.amount <= 1) j++;
    }

    return transfers;
  }, [memberBalances]);

  // 一鍵複製轉帳清單到 LINE
  const handleCopySettlementText = () => {
    if (!currentTrip) return;
    let text = `✈️【${currentTrip.name}】旅費分帳結算通知 ✈️\n`;
    text += `📅 旅程時間：${currentTrip.startDate} ~ ${currentTrip.endDate}\n`;
    text += `--------------------------------\n`;
    text += `💰【最終結清轉帳名單】：\n`;
    if (settlementTransfers.length === 0) {
      text += `全體帳目已平，無須再互相轉帳！🎉\n`;
    } else {
      settlementTransfers.forEach((tr, index) => {
        text += `${index + 1}. ${tr.from}  ➡️  轉帳給【${tr.to}】 NT$ ${tr.amount.toLocaleString()} 元\n`;
      });
    }
    text += `--------------------------------\n`;
    text += `📊【各成員實際總花費】：\n`;
    Object.entries(memberBalances.balances).forEach(([person, data]) => {
      text += `• ${person}：應負擔 NT$ ${data.owed.toLocaleString()} (先代墊 NT$ ${data.paid.toLocaleString()})\n`;
    });
    text += `--------------------------------\n`;
    text += `記帳工具自動計算匯出，收到請核對並及早轉帳唷～感謝旅伴們！✨`;

    navigator.clipboard.writeText(text);
    setCopiedSuccess(true);
    setTimeout(() => setCopiedSuccess(false), 2500);
  };

  // --- 旅程整體花費統計 ---
  const tripTotals = useMemo(() => {
    if (!currentTrip) return {};

    let totalTripTWD = 0;
    let preTripTWD = 0;
    let localTripTWD = 0;
    let foreignCashUsed = 0;
    let totalCardRewardsTWD = 0;
    let cardTWD = 0;
    let cashTWD = 0;

    const categoryBreakdown = {};
    Object.keys(CATEGORY_CONFIG).forEach(k => categoryBreakdown[k] = 0);

    currentTrip.expenses.forEach(item => {
      const twd = convertToTWD(item);
      totalTripTWD += twd;

      if (item.stage === 'pre') preTripTWD += twd;
      else localTripTWD += twd;

      if (item.payMethod === 'card') {
        cardTWD += twd;
        const rewards = calculateCardRewards(item);
        totalCardRewardsTWD += rewards.netRewardTWD;
      } else {
        cashTWD += twd;
        if (item.currency !== 'TWD') {
          foreignCashUsed += Number(item.origAmount || 0);
        }
      }

      if (categoryBreakdown[item.category] !== undefined) {
        categoryBreakdown[item.category] += twd;
      } else {
        categoryBreakdown['其他'] += twd;
      }
    });

    const remainingCash = exchangeStats.totalForeign - foreignCashUsed;

    return {
      totalTripTWD,
      myTotalShareTWD: memberBalances.myTotalShare,
      preTripTWD,
      localTripTWD,
      cardTWD,
      cashTWD,
      foreignCashUsed,
      remainingCash,
      totalCardRewardsTWD,
      categoryBreakdown
    };
  }, [currentTrip, exchangeStats, cards, memberBalances]);

  // --- 記帳 Form 彈窗狀態 ---
  const [isExpenseModalOpen, setIsExpenseModalOpen] = useState(false);
  const [editingExpenseId, setEditingExpenseId] = useState(null);
  const [filterCategory, setFilterCategory] = useState('ALL');
  const [filterMethod, setFilterMethod] = useState('ALL');
  const [searchQuery, setSearchQuery] = useState('');

  const [formData, setFormData] = useState({
    date: new Date().toISOString().split('T')[0],
    stage: 'local',
    category: '食',
    title: '',
    payMethod: 'card',
    cardId: 'dbs-eco',
    currency: 'JPY',
    origAmount: '',
    payer: '我',
    splitType: 'selected_even', // 'self' | 'selected_even' | 'custom_amount' | 'single_reimburse'
    involvedCompanions: ['我'],
    targetCompanion: '',
    customAmounts: {},
    notes: ''
  });

  // 彈窗狀態：旅程、換匯、卡片、旅伴管理
  const [isTripModalOpen, setIsTripModalOpen] = useState(false);
  const [isCompanionModalOpen, setIsCompanionModalOpen] = useState(false);
  const [newCompanionName, setNewCompanionName] = useState('');
  const [newTripData, setNewTripData] = useState({
    name: '',
    startDate: '',
    endDate: '',
    currency: 'JPY',
    currencySymbol: '¥',
    targetBudgetTWD: 65000,
    companions: '我, 佳諭, 逸軒, 傅資深經理'
  });

  const [isExchangeModalOpen, setIsExchangeModalOpen] = useState(false);
  const [newExchange, setNewExchange] = useState({
    date: new Date().toISOString().split('T')[0],
    twdAmount: '',
    foreignAmount: '',
    channel: '星展 Card+ App 換匯'
  });

  const [isCardModalOpen, setIsCardModalOpen] = useState(false);
  const [newCard, setNewCard] = useState({
    name: '星展 頂級商務卡',
    rate: 3.5,
    fee: 1.5,
    notes: '國外消費加碼回饋'
  });

  // 打開新增/修改記帳
  const openExpenseModal = (expense = null) => {
    const allMembers = currentTrip?.companions || ['我'];
    if (expense) {
      setEditingExpenseId(expense.id);
      setFormData({
        ...expense,
        origAmount: expense.origAmount.toString(),
        involvedCompanions: expense.involvedCompanions || allMembers,
        targetCompanion: expense.targetCompanion || allMembers[1] || allMembers[0],
        customAmounts: expense.customAmounts || {}
      });
    } else {
      setEditingExpenseId(null);
      setFormData({
        date: new Date().toISOString().split('T')[0],
        stage: 'local',
        category: '食',
        title: '',
        payMethod: 'card',
        cardId: cards[0]?.id || 'dbs-eco',
        currency: currentTrip?.currency || 'JPY',
        origAmount: '',
        payer: '我',
        splitType: 'selected_even',
        involvedCompanions: [...allMembers], // 預設全員勾選，可取消勾選
        targetCompanion: allMembers[1] || allMembers[0],
        customAmounts: {},
        notes: ''
      });
    }
    setIsExpenseModalOpen(true);
  };

  // 儲存記帳
  const handleSaveExpense = (e) => {
    e.preventDefault();
    if (!formData.title || !formData.origAmount) return;

    const parsedAmount = parseFloat(formData.origAmount);
    const newEntry = {
      ...formData,
      id: editingExpenseId || `exp-${Date.now()}`,
      origAmount: parsedAmount
    };

    setTrips(prev => prev.map(trip => {
      if (trip.id !== activeTripId) return trip;
      let updatedExpenses;
      if (editingExpenseId) {
        updatedExpenses = trip.expenses.map(ex => ex.id === editingExpenseId ? newEntry : ex);
      } else {
        updatedExpenses = [newEntry, ...trip.expenses];
      }
      return { ...trip, expenses: updatedExpenses };
    }));

    setIsExpenseModalOpen(false);
  };

  // 刪除記帳
  const handleDeleteExpense = (id) => {
    setTrips(prev => prev.map(trip => {
      if (trip.id !== activeTripId) return trip;
      return { ...trip, expenses: trip.expenses.filter(ex => ex.id !== id) };
    }));
  };

  // 新增/刪除旅伴
  const handleAddCompanion = (e) => {
    e.preventDefault();
    if (!newCompanionName.trim()) return;
    const name = newCompanionName.trim();
    if (currentTrip.companions.includes(name)) return;

    setTrips(prev => prev.map(t => {
      if (t.id !== activeTripId) return t;
      return { ...t, companions: [...t.companions, name] };
    }));
    setNewCompanionName('');
  };

  const handleRemoveCompanion = (name) => {
    if (name === '我') return; // 保護「我」
    setTrips(prev => prev.map(t => {
      if (t.id !== activeTripId) return t;
      return { ...t, companions: t.companions.filter(c => c !== name) };
    }));
  };

  // 新增換匯紀錄
  const handleAddExchange = (e) => {
    e.preventDefault();
    if (!newExchange.twdAmount || !newExchange.foreignAmount) return;

    const exchangeEntry = {
      id: `ex-${Date.now()}`,
      date: newExchange.date,
      twdAmount: Number(newExchange.twdAmount),
      foreignAmount: Number(newExchange.foreignAmount),
      channel: newExchange.channel || '星展換匯'
    };

    setTrips(prev => prev.map(trip => {
      if (trip.id !== activeTripId) return trip;
      return { ...trip, exchanges: [exchangeEntry, ...(trip.exchanges || [])] };
    }));

    setNewExchange({ date: new Date().toISOString().split('T')[0], twdAmount: '', foreignAmount: '', channel: '星展 Card+ App 換匯' });
    setIsExchangeModalOpen(false);
  };

  const handleDeleteExchange = (id) => {
    setTrips(prev => prev.map(trip => {
      if (trip.id !== activeTripId) return trip;
      return { ...trip, exchanges: trip.exchanges.filter(e => e.id !== id) };
    }));
  };

  // 新增旅程
  const handleCreateTrip = (e) => {
    e.preventDefault();
    if (!newTripData.name) return;

    const companionsArr = newTripData.companions
      .split(',')
      .map(c => c.trim())
      .filter(Boolean);

    const tripObj = {
      id: `trip-${Date.now()}`,
      name: newTripData.name,
      startDate: newTripData.startDate,
      endDate: newTripData.endDate,
      currency: newTripData.currency,
      currencySymbol: newTripData.currencySymbol || '$',
      targetBudgetTWD: Number(newTripData.targetBudgetTWD) || 60000,
      companions: companionsArr.length ? companionsArr : ['我', '小明'],
      exchanges: [],
      expenses: []
    };

    setTrips(prev => [...prev, tripObj]);
    setActiveTripId(tripObj.id);
    setIsTripModalOpen(false);
  };

  // 新增信用卡
  const handleAddCard = (e) => {
    e.preventDefault();
    if (!newCard.name) return;
    const cardObj = {
      id: `dbs-card-${Date.now()}`,
      name: newCard.name,
      rate: Number(newCard.rate) || 2.0,
      fee: Number(newCard.fee) || 1.5,
      notes: newCard.notes
    };
    setCards(prev => [...prev, cardObj]);
    setNewCard({ name: '', rate: 3.0, fee: 1.5, notes: '' });
    setIsCardModalOpen(false);
  };

  // 重設為乾淨空白狀態
  const handleResetSampleData = () => {
    setTrips(CLEAN_INITIAL_TRIPS);
    setCards(DBS_INITIAL_CARDS);
    setActiveTripId(CLEAN_INITIAL_TRIPS[0].id);
  };

  // 匯出 JSON 備份
  const handleExportData = () => {
    const dataStr = "data:text/json;charset=utf-8," + encodeURIComponent(JSON.stringify({ trips, cards }, null, 2));
    const downloadAnchor = document.createElement('a');
    downloadAnchor.setAttribute("href", dataStr);
    downloadAnchor.setAttribute("download", `DBS_TravelBudget_${new Date().toISOString().slice(0,10)}.json`);
    document.body.appendChild(downloadAnchor);
    downloadAnchor.click();
    downloadAnchor.remove();
  };

  // 記帳清單過濾
  const filteredExpenses = useMemo(() => {
    if (!currentTrip) return [];
    return currentTrip.expenses.filter(item => {
      const matchCat = filterCategory === 'ALL' || item.category === filterCategory;
      const matchMethod = filterMethod === 'ALL' || item.payMethod === filterMethod;
      const matchSearch = item.title.toLowerCase().includes(searchQuery.toLowerCase()) ||
                          (item.notes && item.notes.toLowerCase().includes(searchQuery.toLowerCase()));
      return matchCat && matchMethod && matchSearch;
    });
  }, [currentTrip, filterCategory, filterMethod, searchQuery]);

  return (
    <div className="min-h-screen bg-gradient-to-b from-sky-50 via-blue-50/40 to-slate-50 text-slate-800 flex flex-col font-sans selection:bg-sky-500 selection:text-white pb-16">
      {/* 頂部導航列 */}
      <header className="sticky top-0 z-40 bg-white/85 backdrop-blur-md border-b border-sky-100 shadow-xs">
        <div className="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 h-16 flex items-center justify-between">
          <div className="flex items-center space-x-3">
            <div className="w-10 h-10 rounded-xl bg-gradient-to-tr from-sky-500 via-blue-600 to-indigo-600 flex items-center justify-center shadow-md shadow-sky-200">
              <Plane className="w-5 h-5 text-white" />
            </div>
            <div>
              <div className="flex items-center space-x-2">
                <h1 className="text-lg font-bold tracking-tight text-slate-900">
                  旅遊記帳
                </h1>
              </div>
              <p className="text-xs text-slate-500">出國花費 • 換匯計算 • 旅伴分帳</p>
            </div>
          </div>

          <div className="flex items-center space-x-2">
            <button
              onClick={handleExportData}
              title="備份匯出 JSON"
              className="p-2 text-slate-500 hover:text-sky-600 hover:bg-sky-50 rounded-lg transition"
            >
              <Download className="w-4 h-4" />
            </button>
            <button
              onClick={handleResetSampleData}
              title="重載範例資料"
              className="p-2 text-slate-500 hover:text-sky-600 hover:bg-sky-50 rounded-lg transition"
            >
              <RefreshCw className="w-4 h-4" />
            </button>
            <button
              onClick={() => setIsTripModalOpen(true)}
              className="flex items-center space-x-1.5 px-3 py-1.5 bg-gradient-to-r from-sky-600 to-blue-600 hover:from-sky-500 hover:to-blue-500 text-white rounded-lg text-xs font-semibold shadow-sm shadow-sky-200"
            >
              <Plus className="w-3.5 h-3.5" />
              <span>新旅程</span>
            </button>
          </div>
        </div>
      </header>

      {/* 主體區塊 */}
      <main className="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-6 w-full flex-1">
        {/* 旅程切換 Bar */}
        <div className="flex flex-col sm:flex-row sm:items-center justify-between gap-4 mb-6">
          <div className="flex items-center space-x-2 overflow-x-auto pb-2 sm:pb-0 scrollbar-thin">
            <span className="text-xs font-semibold text-slate-500 uppercase tracking-wider whitespace-nowrap mr-1">
              當前旅程：
            </span>
            {trips.map(trip => {
              const isActive = trip.id === activeTripId;
              return (
                <button
                  key={trip.id}
                  onClick={() => setActiveTripId(trip.id)}
                  className={`px-4 py-2 rounded-xl text-sm font-medium whitespace-nowrap transition-all duration-200 flex items-center space-x-2 border ${
                    isActive
                      ? 'bg-gradient-to-r from-sky-500 to-blue-600 text-white border-transparent shadow-md shadow-sky-200'
                      : 'bg-white text-slate-700 border-sky-100 hover:bg-sky-50/70 hover:border-sky-200'
                  }`}
                >
                  <MapPin className="w-3.5 h-3.5" />
                  <span>{trip.name}</span>
                  <span className={`text-xs px-1.5 py-0.5 rounded-full ${isActive ? 'bg-white/20 text-white font-semibold' : 'bg-sky-50 text-sky-700'}`}>
                    {trip.currency}
                  </span>
                </button>
              );
            })}
          </div>

          {currentTrip && (
            <div className="flex items-center space-x-3 bg-white px-3.5 py-2 rounded-xl border border-sky-100 shadow-xs self-start sm:self-auto text-xs">
              <span className="flex items-center text-slate-500">
                <Calendar className="w-3.5 h-3.5 mr-1 text-sky-500" />
                {currentTrip.startDate} ~ {currentTrip.endDate}
              </span>
              <span className="text-slate-300">|</span>
              <button
                onClick={() => setIsCompanionModalOpen(true)}
                className="flex items-center text-slate-600 hover:text-sky-600"
              >
                <Users className="w-3.5 h-3.5 mr-1 text-sky-500" />
                <span>成員 ({currentTrip.companions?.length}人): {currentTrip.companions?.join(', ')}</span>
                <span className="ml-1 text-[10px] text-sky-600 font-semibold underline">編輯</span>
              </button>
            </div>
          )}
        </div>

        {/* 核心數據看板 (指標卡) */}
        {currentTrip && (
          <div className="grid grid-cols-2 md:grid-cols-3 lg:grid-cols-6 gap-3 mb-6">
            {/* 卡片 1: 總花費 */}
            <div className="bg-white border border-sky-100 p-3.5 rounded-2xl shadow-xs">
              <div className="text-xs text-slate-500 font-medium">旅程帳面總開銷</div>
              <div className="text-xl font-bold text-slate-900 mt-1">
                ${tripTotals.totalTripTWD?.toLocaleString()} <span className="text-xs font-normal text-slate-400">TWD</span>
              </div>
              <div className="text-[11px] text-slate-400 mt-1">
                預算: ${currentTrip.targetBudgetTWD?.toLocaleString()}
              </div>
            </div>

            {/* 卡片 2: 我個人應付 */}
            <div className="bg-gradient-to-b from-sky-50/80 to-white border border-sky-200 p-3.5 rounded-2xl shadow-xs">
              <div className="text-xs text-sky-800 font-semibold flex items-center">
                <CheckCircle className="w-3.5 h-3.5 mr-1 text-sky-600" />
                我個人實質支出
              </div>
              <div className="text-xl font-bold text-sky-900 mt-1">
                ${tripTotals.myTotalShareTWD?.toLocaleString()} <span className="text-xs font-normal text-sky-600">TWD</span>
              </div>
              <div className="text-[11px] text-sky-600/80 mt-1">
                已精算分攤與代墊後
              </div>
            </div>

            {/* 卡片 3: 行前預付 (機票住宿提前刷) */}
            <div className="bg-white border border-sky-100 p-3.5 rounded-2xl shadow-xs">
              <div className="text-xs text-blue-600 font-medium flex items-center">
                <Sparkles className="w-3 h-3 mr-1 text-blue-500" />
                提前預付 (機酒)
              </div>
              <div className="text-xl font-bold text-slate-900 mt-1">
                ${tripTotals.preTripTWD?.toLocaleString()} <span className="text-xs font-normal text-slate-400">TWD</span>
              </div>
              <div className="text-[11px] text-slate-500 mt-1">
                當地現場: ${tripTotals.localTripTWD?.toLocaleString()}
              </div>
            </div>

            {/* 卡片 4: 星展海外回饋淨賺 */}
            <div className="bg-gradient-to-b from-emerald-50/60 to-white border border-emerald-200/80 p-3.5 rounded-2xl shadow-xs">
              <div className="text-xs text-emerald-800 font-semibold flex items-center">
                <TrendingUp className="w-3 h-3 mr-1 text-emerald-600" />
                星展回饋淨賺
              </div>
              <div className="text-xl font-bold text-emerald-700 mt-1">
                +${tripTotals.totalCardRewardsTWD?.toLocaleString()} <span className="text-xs font-normal text-emerald-600">TWD</span>
              </div>
              <div className="text-[11px] text-emerald-600/80 mt-1">
                已扣除 1.5% 海外手續費
              </div>
            </div>

            {/* 卡片 5: 加權實質匯率 */}
            <div 
              className="bg-white border border-sky-100 p-3.5 rounded-2xl shadow-xs cursor-pointer hover:border-sky-300 transition"
              onClick={() => setActiveTab('exchange')}
            >
              <div className="text-xs text-amber-700 font-medium flex items-center justify-between">
                <span>實質加權匯率</span>
                <ArrowRightLeft className="w-3 h-3 text-amber-500" />
              </div>
              <div className="text-xl font-bold text-amber-800 mt-1">
                {exchangeStats.avgRate ? exchangeStats.avgRate.toFixed(4) : '--'}
              </div>
              <div className="text-[11px] text-slate-500 mt-1 truncate">
                已換匯 ${exchangeStats.totalTwd.toLocaleString()} TWD
              </div>
            </div>

            {/* 卡片 6: 外幣現鈔庫存 */}
            <div className="bg-white border border-sky-100 p-3.5 rounded-2xl shadow-xs">
              <div className="text-xs text-indigo-700 font-medium flex items-center">
                <Wallet className="w-3 h-3 mr-1 text-indigo-500" />
                外幣現鈔剩餘
              </div>
              <div className="text-xl font-bold text-indigo-900 mt-1">
                {currentTrip.currencySymbol}{tripTotals.remainingCash?.toLocaleString()}
              </div>
              <div className="text-[11px] text-slate-500 mt-1">
                已付現 {currentTrip.currencySymbol}{tripTotals.foreignCashUsed?.toLocaleString()}
              </div>
            </div>
          </div>
        )}

        {/* 頁籤切換 */}
        <div className="flex border-b border-sky-100 mb-6 gap-2 overflow-x-auto scrollbar-thin">
          {[
            { id: 'expenses', label: '記帳明細清單', icon: DollarSign },
            { id: 'split', label: '旅伴分帳與LINE結算', icon: Users, badge: settlementTransfers.length > 0 ? `${settlementTransfers.length}筆轉帳` : null },
            { id: 'analytics', label: '費用統計報表', icon: PieChart },
            { id: 'exchange', label: '換匯記錄與現鈔', icon: ArrowRightLeft },
            { id: 'cards', label: '星展信用卡試算庫', icon: CreditCard },
          ].map(tab => {
            const Icon = tab.icon;
            const isActive = activeTab === tab.id;
            return (
              <button
                key={tab.id}
                onClick={() => setActiveTab(tab.id)}
                className={`flex items-center space-x-2 py-3 px-4 text-xs font-semibold border-b-2 transition -mb-[1px] whitespace-nowrap ${
                  isActive
                    ? 'border-sky-600 text-sky-700 bg-white rounded-t-xl shadow-xs'
                    : 'border-transparent text-slate-500 hover:text-sky-700 hover:border-sky-200'
                }`}
              >
                <Icon className="w-4 h-4" />
                <span>{tab.label}</span>
                {tab.badge && (
                  <span className="px-1.5 py-0.2 rounded-full text-[10px] bg-sky-100 text-sky-800 border border-sky-200 font-bold">
                    {tab.badge}
                  </span>
                )}
              </button>
            );
          })}
        </div>

        {/* --- TAB 1: 記帳明細列表 --- */}
        {activeTab === 'expenses' && (
          <div className="space-y-4">
            {/* 篩選與新增控制列 */}
            <div className="bg-white border border-sky-100 p-3 rounded-2xl flex flex-wrap items-center justify-between gap-3 shadow-xs">
              <div className="flex items-center space-x-2 flex-1 min-w-[200px]">
                <div className="relative w-full max-w-xs">
                  <Search className="w-4 h-4 text-slate-400 absolute left-3 top-1/2 -translate-y-1/2" />
                  <input
                    type="text"
                    value={searchQuery}
                    onChange={(e) => setSearchQuery(e.target.value)}
                    placeholder="搜尋品項或備註 (例如機票、燒肉)..."
                    className="w-full bg-slate-50 border border-sky-100 rounded-xl pl-9 pr-3 py-1.5 text-xs text-slate-800 placeholder-slate-400 focus:outline-none focus:border-sky-500 focus:bg-white"
                  />
                </div>
              </div>

              <div className="flex items-center space-x-2">
                <select
                  value={filterCategory}
                  onChange={(e) => setFilterCategory(e.target.value)}
                  className="bg-slate-50 border border-sky-100 rounded-xl px-2.5 py-1.5 text-xs text-slate-700 focus:outline-none focus:border-sky-400"
                >
                  <option value="ALL">全部分類</option>
                  {Object.keys(CATEGORY_CONFIG).map(c => (
                    <option key={c} value={c}>{c}</option>
                  ))}
                </select>

                <select
                  value={filterMethod}
                  onChange={(e) => setFilterMethod(e.target.value)}
                  className="bg-slate-50 border border-sky-100 rounded-xl px-2.5 py-1.5 text-xs text-slate-700 focus:outline-none focus:border-sky-400"
                >
                  <option value="ALL">全部支付方式</option>
                  <option value="card">刷卡</option>
                  <option value="cash">現金</option>
                </select>

                <button
                  onClick={() => openExpenseModal()}
                  className="flex items-center space-x-1 px-4 py-1.5 bg-gradient-to-r from-sky-500 to-blue-600 hover:from-sky-600 hover:to-blue-700 text-white rounded-xl text-xs font-semibold shadow-sm shadow-sky-200"
                >
                  <Plus className="w-4 h-4" />
                  <span>記一筆</span>
                </button>
              </div>
            </div>

            {/* 明細清單 */}
            <div className="bg-white border border-sky-100 rounded-2xl overflow-hidden divide-y divide-sky-50 shadow-xs">
              {filteredExpenses.length === 0 ? (
                <div className="p-12 text-center text-slate-400 text-xs">
                  <DollarSign className="w-10 h-10 mx-auto text-sky-200 mb-2 stroke-[1.5]" />
                  <p>尚無符合條件的支出紀錄</p>
                  <button
                    onClick={() => openExpenseModal()}
                    className="mt-3 text-xs text-sky-600 font-semibold hover:underline"
                  >
                    點擊新增第一筆消費 (支援提前買機票或當地分攤)
                  </button>
                </div>
              ) : (
                filteredExpenses.map((item) => {
                  const catConfig = CATEGORY_CONFIG[item.category] || CATEGORY_CONFIG['其他'];
                  const Icon = catConfig.icon;
                  const twdAmount = convertToTWD(item);
                  const rewards = calculateCardRewards(item);

                  return (
                    <div
                      key={item.id}
                      className="p-4 hover:bg-sky-50/50 transition flex items-center justify-between group"
                    >
                      {/* 左側：圖示 + 標題資訊 */}
                      <div className="flex items-center space-x-3.5">
                        <div className={`w-11 h-11 rounded-2xl flex items-center justify-center ${catConfig.bg} ${catConfig.border} border shadow-2xs`}>
                          <Icon className="w-5 h-5" />
                        </div>
                        <div>
                          <div className="flex items-center space-x-2">
                            <span className="font-semibold text-sm text-slate-900">{item.title}</span>
                            {item.stage === 'pre' && (
                              <span className="px-2 py-0.5 text-[10px] bg-blue-50 text-blue-700 border border-blue-200 rounded-full font-medium">
                                行前預付
                              </span>
                            )}
                            <span className="text-[11px] text-slate-400">{item.date}</span>
                          </div>

                          <div className="flex flex-wrap items-center gap-2 mt-1 text-xs text-slate-500">
                            {/* 支付與卡片標籤 */}
                            {item.payMethod === 'card' ? (
                              <span className="inline-flex items-center text-sky-800 bg-sky-50 border border-sky-200 px-2 py-0.5 rounded text-[11px]">
                                <CreditCard className="w-3 h-3 mr-1 text-sky-600" />
                                {rewards.cardName}
                                {rewards.rate && (
                                  <span className="ml-1 text-emerald-600 font-semibold">
                                    (淨賺 +${rewards.netRewardTWD})
                                  </span>
                                )}
                              </span>
                            ) : (
                              <span className="inline-flex items-center text-amber-800 bg-amber-50 border border-amber-200 px-2 py-0.5 rounded text-[11px]">
                                <Wallet className="w-3 h-3 mr-1 text-amber-600" />
                                外幣現鈔支付
                              </span>
                            )}

                            {/* 付款人與分攤模式摘要 */}
                            <span className="text-slate-600">
                              由 <strong className="text-slate-900">{item.payer}</strong> 先付
                            </span>
                            <span className="text-slate-300">•</span>

                            {/* 分攤標籤解析 */}
                            {item.splitType === 'self' && (
                              <span className="text-slate-500">個人全自費</span>
                            )}
                            {item.splitType === 'selected_even' && (
                              <span className="text-blue-700 bg-blue-50 px-2 py-0.5 rounded border border-blue-200 text-[11px] font-medium">
                                平分成員 ({item.involvedCompanions?.length}人)：{item.involvedCompanions?.join(', ')}
                              </span>
                            )}
                            {item.splitType === 'custom_amount' && (
                              <span className="text-amber-800 bg-amber-50 px-2 py-0.5 rounded border border-amber-200 text-[11px] font-medium">
                                自訂金額分攤
                              </span>
                            )}
                            {item.splitType === 'single_reimburse' && (
                              <span className="text-indigo-700 bg-indigo-50 px-2 py-0.5 rounded border border-indigo-200 text-[11px] font-medium">
                                專為【{item.targetCompanion}】代墊
                              </span>
                            )}

                            {item.notes && (
                              <span className="text-slate-400 italic max-w-xs truncate">
                                "{item.notes}"
                              </span>
                            )}
                          </div>
                        </div>
                      </div>

                      {/* 右側：金額與操作按鈕 */}
                      <div className="flex items-center space-x-4">
                        <div className="text-right">
                          <div className="text-base font-bold text-slate-900">
                            ${twdAmount.toLocaleString()} <span className="text-xs font-normal text-slate-400">TWD</span>
                          </div>
                          {item.currency !== 'TWD' && (
                            <div className="text-xs text-slate-500">
                              {item.currency} {Number(item.origAmount).toLocaleString()}
                            </div>
                          )}
                        </div>

                        {/* 動作按鈕 */}
                        <div className="flex items-center space-x-1 opacity-0 group-hover:opacity-100 transition">
                          <button
                            onClick={() => openExpenseModal(item)}
                            className="p-1.5 text-slate-400 hover:text-sky-600 hover:bg-sky-50 rounded-lg"
                            title="編輯"
                          >
                            <Edit3 className="w-4 h-4" />
                          </button>
                          <button
                            onClick={() => handleDeleteExpense(item.id)}
                            className="p-1.5 text-slate-400 hover:text-rose-500 hover:bg-rose-50 rounded-lg"
                            title="刪除"
                          >
                            <Trash2 className="w-4 h-4" />
                          </button>
                        </div>
                      </div>
                    </div>
                  );
                })
              )}
            </div>
          </div>
        )}

        {/* --- TAB 2: 旅伴分帳結算與LINE一鍵複製 --- */}
        {activeTab === 'split' && currentTrip && (
          <div className="space-y-6">
            {/* 上半部：LINE 快速結算卡片 */}
            <div className="bg-gradient-to-r from-sky-50 via-blue-50/70 to-indigo-50/60 border border-sky-200 p-5 rounded-2xl flex flex-col md:flex-row items-start md:items-center justify-between gap-4 shadow-xs">
              <div>
                <div className="flex items-center space-x-2">
                  <h3 className="text-base font-bold text-slate-900 flex items-center">
                    <Users className="w-5 h-5 mr-2 text-sky-600" />
                    旅途結算：最佳化找補轉帳名單
                  </h3>
                  <span className="text-xs bg-emerald-100 text-emerald-800 px-2 py-0.5 rounded-full border border-emerald-200 font-semibold">
                    已自動對沖代墊款
                  </span>
                </div>
                <p className="text-xs text-slate-600 mt-1 max-w-2xl leading-relaxed">
                  系統自動依每筆消費勾選的成員（未吃不分攤、各自付、代買）進行對沖，產生最少轉帳次數的找補方案，不用再逐筆算數學！
                </p>
              </div>

              <button
                onClick={handleCopySettlementText}
                className="flex items-center space-x-2 px-4 py-2.5 bg-gradient-to-r from-emerald-600 to-teal-600 hover:from-emerald-500 hover:to-teal-500 text-white rounded-xl text-xs font-bold whitespace-nowrap shadow-md shadow-emerald-200 transition"
              >
                {copiedSuccess ? <Check className="w-4 h-4 text-emerald-100" /> : <Copy className="w-4 h-4" />}
                <span>{copiedSuccess ? '已複製到剪貼簿！' : '一鍵複製 LINE 結算清單'}</span>
              </button>
            </div>

            {/* 轉帳任務卡片列表 */}
            <div className="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-4">
              {settlementTransfers.length === 0 ? (
                <div className="col-span-full bg-white border border-sky-100 p-8 rounded-2xl text-center text-slate-500 text-xs shadow-xs">
                  <CheckCircle className="w-8 h-8 mx-auto text-emerald-500 mb-2" />
                  太棒了！所有旅伴目前的代墊與應付金額剛好平衡，無人需進行額外轉帳。
                </div>
              ) : (
                settlementTransfers.map((item, index) => (
                  <div
                    key={index}
                    className="bg-white border border-sky-100 p-4 rounded-2xl relative overflow-hidden flex flex-col justify-between shadow-xs hover:border-sky-300 transition"
                  >
                    <div>
                      <div className="flex items-center justify-between text-xs text-slate-500">
                        <span className="font-semibold text-slate-700">轉帳找補 #{index + 1}</span>
                        <span className="text-[10px] bg-sky-50 text-sky-700 px-2 py-0.5 rounded-full border border-sky-100">
                          網銀 / 街口 / LINE Pay
                        </span>
                      </div>

                      <div className="mt-3 flex items-center justify-between bg-sky-50/60 p-3 rounded-xl border border-sky-100">
                        <div className="text-center flex-1">
                          <span className="text-[10px] text-rose-600 block font-semibold">轉出者</span>
                          <span className="text-sm font-bold text-slate-900 mt-0.5 block">{item.from}</span>
                        </div>
                        <div className="px-2 text-sky-600 font-bold">➡️</div>
                        <div className="text-center flex-1">
                          <span className="text-[10px] text-emerald-700 block font-semibold">收款人</span>
                          <span className="text-sm font-bold text-slate-900 mt-0.5 block">{item.to}</span>
                        </div>
                      </div>
                    </div>

                    <div className="mt-4 pt-3 border-t border-sky-50 flex items-center justify-between">
                      <span className="text-xs text-slate-500">應還款金額：</span>
                      <span className="text-lg font-bold text-emerald-700">
                        ${item.amount.toLocaleString()} <span className="text-xs font-normal text-slate-500">TWD</span>
                      </span>
                    </div>
                  </div>
                ))
              )}
            </div>

            {/* 下半部：各成員代墊與花費明細盤點 */}
            <div className="bg-white border border-sky-100 p-5 rounded-2xl shadow-xs">
              <h4 className="text-sm font-semibold text-slate-900 mb-4">每位成員收支對帳盤點表</h4>
              <div className="divide-y divide-sky-50 text-xs">
                <div className="py-2 grid grid-cols-4 font-semibold text-slate-500">
                  <span>旅伴姓名</span>
                  <span>先墊付總金額 (出資)</span>
                  <span>實際應負擔總額 (享受)</span>
                  <span className="text-right">最終淨額結算</span>
                </div>
                {Object.entries(memberBalances.balances).map(([name, data]) => {
                  const isPositive = data.net > 0;
                  const isZero = Math.abs(data.net) <= 1;

                  return (
                    <div key={name} className="py-3 grid grid-cols-4 items-center">
                      <span className="font-bold text-slate-800">{name}</span>
                      <span className="text-slate-600">${data.paid.toLocaleString()}</span>
                      <span className="text-slate-600">${data.owed.toLocaleString()}</span>
                      <div className="text-right">
                        <span className={`font-bold px-2 py-0.5 rounded text-xs ${
                          isPositive
                            ? 'text-emerald-700 bg-emerald-50 border border-emerald-200'
                            : isZero
                            ? 'text-slate-500 bg-slate-100'
                            : 'text-rose-700 bg-rose-50 border border-rose-200'
                        }`}>
                          {isPositive && `應收款 +$${data.net.toLocaleString()}`}
                          {!isPositive && !isZero && `應轉出 -$${Math.abs(data.net).toLocaleString()}`}
                          {isZero && '結清 (0)'}
                        </span>
                      </div>
                    </div>
                  );
                })}
              </div>
            </div>
          </div>
        )}

        {/* --- TAB 3: 費用統計分析 --- */}
        {activeTab === 'analytics' && currentTrip && (
          <div className="grid grid-cols-1 lg:grid-cols-3 gap-6">
            <div className="lg:col-span-2 bg-white border border-sky-100 p-5 rounded-2xl shadow-xs">
              <h3 className="text-base font-semibold text-slate-900 mb-4 flex items-center">
                <PieChart className="w-4 h-4 mr-2 text-sky-600" />
                項目類別支出佔比
              </h3>

              <div className="space-y-3.5">
                {Object.entries(tripTotals.categoryBreakdown).map(([cat, amount]) => {
                  const percent = tripTotals.totalTripTWD > 0
                    ? Math.round((amount / tripTotals.totalTripTWD) * 100)
                    : 0;
                  const catConfig = CATEGORY_CONFIG[cat] || CATEGORY_CONFIG['其他'];
                  const Icon = catConfig.icon;

                  return (
                    <div key={cat} className="space-y-1">
                      <div className="flex items-center justify-between text-xs">
                        <div className="flex items-center space-x-2">
                          <Icon className="w-3.5 h-3.5 text-sky-600" />
                          <span className="text-slate-700 font-medium">{cat}</span>
                        </div>
                        <div className="text-slate-800">
                          ${amount.toLocaleString()} TWD{' '}
                          <span className="text-slate-400 font-normal">({percent}%)</span>
                        </div>
                      </div>
                      <div className="w-full bg-slate-100 h-2 rounded-full overflow-hidden">
                        <div
                          className="h-full bg-gradient-to-r from-sky-500 to-blue-600 rounded-full transition-all duration-500"
                          style={{ width: `${percent}%` }}
                        />
                      </div>
                    </div>
                  );
                })}
              </div>
            </div>

            <div className="space-y-6">
              {/* 支付方式比例 */}
              <div className="bg-white border border-sky-100 p-5 rounded-2xl shadow-xs">
                <h3 className="text-base font-semibold text-slate-900 mb-3">支付管道比例</h3>
                <div className="space-y-3 text-xs">
                  <div>
                    <div className="flex justify-between text-slate-700 mb-1">
                      <span>星展信用卡支付</span>
                      <span className="font-semibold">${tripTotals.cardTWD?.toLocaleString()} TWD</span>
                    </div>
                    <div className="w-full bg-slate-100 h-2 rounded-full overflow-hidden">
                      <div
                        className="h-full bg-sky-500"
                        style={{
                          width: `${tripTotals.totalTripTWD ? Math.round((tripTotals.cardTWD / tripTotals.totalTripTWD) * 100) : 0}%`
                        }}
                      />
                    </div>
                  </div>

                  <div>
                    <div className="flex justify-between text-slate-700 mb-1">
                      <span>外幣現金支付</span>
                      <span className="font-semibold">${tripTotals.cashTWD?.toLocaleString()} TWD</span>
                    </div>
                    <div className="w-full bg-slate-100 h-2 rounded-full overflow-hidden">
                      <div
                        className="h-full bg-amber-500"
                        style={{
                          width: `${tripTotals.totalTripTWD ? Math.round((tripTotals.cashTWD / tripTotals.totalTripTWD) * 100) : 0}%`
                        }}
                      />
                    </div>
                  </div>
                </div>

                <div className="mt-4 p-3 rounded-xl bg-sky-50/70 border border-sky-100 text-[11px] text-slate-600 leading-relaxed">
                  💡 星展刷卡小秘訣：在日本、韓國或歐美實體店家，強烈推薦刷 <strong>星展 eco 永續卡</strong>（享 5% 加碼，扣除 1.5% 手續費現賺 3.5%）；大額購買機票則可刷 <strong>星展飛行卡</strong> 快速累積航空哩程！
                </div>
              </div>

              {/* 階段統計 */}
              <div className="bg-white border border-sky-100 p-5 rounded-2xl shadow-xs">
                <h3 className="text-base font-semibold text-slate-900 mb-3">支出時間結構</h3>
                <div className="grid grid-cols-2 gap-3 text-center">
                  <div className="p-3 bg-sky-50/50 rounded-xl border border-sky-100">
                    <span className="text-xs text-blue-700 font-semibold">行前預購支出</span>
                    <div className="text-lg font-bold text-slate-900 mt-1">
                      ${tripTotals.preTripTWD?.toLocaleString()}
                    </div>
                    <span className="text-[10px] text-slate-500">機票 / 飯店 / 門票</span>
                  </div>
                  <div className="p-3 bg-sky-50/50 rounded-xl border border-sky-100">
                    <span className="text-xs text-sky-700 font-semibold">當地即時開銷</span>
                    <div className="text-lg font-bold text-slate-900 mt-1">
                      ${tripTotals.localTripTWD?.toLocaleString()}
                    </div>
                    <span className="text-[10px] text-slate-500">美食 / 交通 / 購物</span>
                  </div>
                </div>
              </div>
            </div>
          </div>
        )}

        {/* --- TAB 4: 換匯記錄與現金庫存 --- */}
        {activeTab === 'exchange' && currentTrip && (
          <div className="space-y-6">
            <div className="bg-gradient-to-r from-amber-50 via-sky-50/60 to-white border border-amber-200/80 p-5 rounded-2xl flex flex-col md:flex-row items-start md:items-center justify-between gap-4 shadow-xs">
              <div>
                <h3 className="text-base font-bold text-amber-900 flex items-center">
                  <ArrowRightLeft className="w-5 h-5 mr-2 text-amber-600" />
                  外幣加權平均換匯機制 ({currentTrip.currency})
                </h3>
                <p className="text-xs text-slate-600 mt-1 max-w-2xl leading-relaxed">
                  出國前分批透過星展網銀或臨櫃提領現鈔，每次匯率都不同。系統會自動加總「總支出台幣 ÷ 總換得外幣」，得出這趟旅程的<strong>加權實質匯率 ({exchangeStats.avgRate.toFixed(4)})</strong>。
                  所有外幣消費皆以此匯率折算台幣，帳目最貼近真實花費！
                </p>
              </div>

              <button
                onClick={() => setIsExchangeModalOpen(true)}
                className="px-4 py-2 bg-gradient-to-r from-amber-500 to-amber-600 hover:from-amber-600 hover:to-amber-700 text-white rounded-xl text-xs font-semibold whitespace-nowrap shadow-sm shadow-amber-200"
              >
                + 記錄一筆換匯
              </button>
            </div>

            {/* 換匯清單 */}
            <div className="bg-white border border-sky-100 rounded-2xl overflow-hidden shadow-xs">
              <div className="px-5 py-3.5 border-b border-sky-100 font-semibold text-xs text-slate-500 grid grid-cols-5 bg-sky-50/30">
                <span>換匯日期</span>
                <span>支出台幣 (TWD)</span>
                <span>換得外幣 ({currentTrip.currency})</span>
                <span>實質匯率</span>
                <span className="text-right">換匯管道 / 備註</span>
              </div>

              <div className="divide-y divide-sky-50">
                {currentTrip.exchanges && currentTrip.exchanges.length > 0 ? (
                  currentTrip.exchanges.map((ex) => {
                    const rate = ex.foreignAmount > 0 ? (ex.twdAmount / ex.foreignAmount).toFixed(4) : '--';
                    return (
                      <div key={ex.id} className="px-5 py-3 text-xs grid grid-cols-5 items-center hover:bg-sky-50/50">
                        <span className="text-slate-600">{ex.date}</span>
                        <span className="font-semibold text-slate-900">${ex.twdAmount?.toLocaleString()}</span>
                        <span className="font-semibold text-amber-700">
                          {currentTrip.currencySymbol}{ex.foreignAmount?.toLocaleString()}
                        </span>
                        <span className="text-slate-600">{rate}</span>
                        <div className="flex items-center justify-end space-x-2">
                          <span className="text-slate-500 truncate">{ex.channel}</span>
                          <button
                            onClick={() => handleDeleteExchange(ex.id)}
                            className="text-slate-400 hover:text-rose-500 p-1"
                          >
                            <Trash2 className="w-3.5 h-3.5" />
                          </button>
                        </div>
                      </div>
                    );
                  })
                ) : (
                  <div className="p-8 text-center text-slate-400 text-xs">
                    尚未新增任何換匯紀錄，可點擊上方按鈕記錄提領或星展線上換匯明細。
                  </div>
                )}
              </div>
            </div>
          </div>
        )}

        {/* --- TAB 5: 星展信用卡庫與試算 --- */}
        {activeTab === 'cards' && (
          <div className="space-y-6">
            <div className="flex items-center justify-between">
              <div>
                <h3 className="text-base font-semibold text-slate-900">星展銀行 (DBS) 海外神卡庫與回饋試算</h3>
                <p className="text-xs text-slate-500 mt-0.5">預設已包含星展主力神卡回饋與 1.5% 海外手續費設定，可依您手上的卡別自訂修改。</p>
              </div>
              <button
                onClick={() => setIsCardModalOpen(true)}
                className="flex items-center space-x-1 px-3 py-1.5 bg-gradient-to-r from-sky-500 to-blue-600 hover:from-sky-600 hover:to-blue-700 text-white rounded-xl text-xs font-semibold shadow-xs"
              >
                <Plus className="w-3.5 h-3.5" />
                <span>新增卡片</span>
              </button>
            </div>

            <div className="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-4">
              {cards.map((card) => {
                const netRate = (card.rate - card.fee).toFixed(1);
                return (
                  <div
                    key={card.id}
                    className="bg-white border border-sky-100 p-4 rounded-2xl relative overflow-hidden flex flex-col justify-between shadow-xs hover:border-sky-300 transition"
                  >
                    <div>
                      <div className="flex items-start justify-between">
                        <div className="flex items-center space-x-2">
                          <div className="w-8 h-8 rounded-lg bg-sky-50 text-sky-600 border border-sky-100 flex items-center justify-center">
                            <CreditCard className="w-4 h-4" />
                          </div>
                          <div>
                            <h4 className="font-semibold text-sm text-slate-900">{card.name}</h4>
                            <span className="text-[11px] text-slate-500">海外手續費: {card.fee}%</span>
                          </div>
                        </div>
                        <div className="text-right">
                          <span className="text-lg font-bold text-sky-600">{card.rate}%</span>
                          <div className="text-[10px] text-slate-400">回饋率/價值</div>
                        </div>
                      </div>

                      <div className="mt-4 p-2.5 bg-sky-50/50 rounded-xl border border-sky-100 text-xs text-slate-700">
                        <div className="flex justify-between items-center mb-1">
                          <span className="text-slate-500">扣除手續費淨賺率：</span>
                          <span className="font-bold text-emerald-600">+{netRate}%</span>
                        </div>
                        <p className="text-[11px] text-slate-500 mt-1">{card.notes || '無特殊備註'}</p>
                      </div>
                    </div>

                    <div className="mt-4 pt-3 border-t border-sky-50 flex items-center justify-between text-xs text-slate-500">
                      <span>當前旅程已刷：</span>
                      <span className="font-semibold text-slate-900">
                        $
                        {currentTrip?.expenses
                          .filter(e => e.payMethod === 'card' && e.cardId === card.id)
                          .reduce((s, e) => s + convertToTWD(e), 0)
                          .toLocaleString()}{' '}
                        TWD
                      </span>
                    </div>
                  </div>
                );
              })}
            </div>
          </div>
        )}
      </main>

      {/* --- MODAL 1: 新增 / 編輯 記帳明細 --- */}
      {isExpenseModalOpen && (
        <div className="fixed inset-0 z-50 flex items-center justify-center p-4 bg-slate-900/40 backdrop-blur-sm animate-in fade-in duration-150">
          <div className="bg-white border border-sky-100 rounded-3xl max-w-lg w-full p-6 shadow-2xl overflow-y-auto max-h-[92vh]">
            <div className="flex items-center justify-between pb-3 border-b border-sky-100">
              <h3 className="text-base font-bold text-slate-900 flex items-center">
                <DollarSign className="w-4 h-4 mr-2 text-sky-600" />
                {editingExpenseId ? '編輯消費項目' : '新增消費項目'}
              </h3>
              <button
                onClick={() => setIsExpenseModalOpen(false)}
                className="text-slate-400 hover:text-slate-700 text-sm"
              >
                ✕
              </button>
            </div>

            <form onSubmit={handleSaveExpense} className="mt-4 space-y-4 text-xs">
              {/* 日期與階段 (行前預付 vs 當地) */}
              <div className="grid grid-cols-2 gap-3">
                <div>
                  <label className="block text-slate-600 mb-1 font-semibold">消費日期 (支援提前付款)</label>
                  <input
                    type="date"
                    required
                    value={formData.date}
                    onChange={(e) => setFormData({ ...formData, date: e.target.value })}
                    className="w-full bg-slate-50 border border-sky-100 rounded-xl px-3 py-2 text-slate-800 focus:outline-none focus:border-sky-500 focus:bg-white"
                  />
                </div>
                <div>
                  <label className="block text-slate-600 mb-1 font-semibold">消費階段</label>
                  <select
                    value={formData.stage}
                    onChange={(e) => setFormData({ ...formData, stage: e.target.value })}
                    className="w-full bg-slate-50 border border-sky-100 rounded-xl px-3 py-2 text-slate-800 focus:outline-none focus:border-sky-500 focus:bg-white"
                  >
                    <option value="pre">行前準備 (提前買機票、住宿、門票)</option>
                    <option value="local">當地即時開銷 (餐飲、交通、購物)</option>
                  </select>
                </div>
              </div>

              {/* 分類與品項名稱 */}
              <div className="grid grid-cols-3 gap-3">
                <div>
                  <label className="block text-slate-600 mb-1 font-semibold">項目類別</label>
                  <select
                    value={formData.category}
                    onChange={(e) => setFormData({ ...formData, category: e.target.value })}
                    className="w-full bg-slate-50 border border-sky-100 rounded-xl px-3 py-2 text-slate-800 focus:outline-none focus:border-sky-500 focus:bg-white"
                  >
                    {Object.keys(CATEGORY_CONFIG).map((c) => (
                      <option key={c} value={c}>{c}</option>
                    ))}
                  </select>
                </div>
                <div className="col-span-2">
                  <label className="block text-slate-600 mb-1 font-semibold">品項名稱</label>
                  <input
                    type="text"
                    required
                    placeholder="例如：成田特快、一蘭拉麵、燒肉套餐"
                    value={formData.title}
                    onChange={(e) => setFormData({ ...formData, title: e.target.value })}
                    className="w-full bg-slate-50 border border-sky-100 rounded-xl px-3 py-2 text-slate-800 focus:outline-none focus:border-sky-500 focus:bg-white"
                  />
                </div>
              </div>

              {/* 幣別與金額 */}
              <div className="grid grid-cols-3 gap-3">
                <div>
                  <label className="block text-slate-600 mb-1 font-semibold">幣別</label>
                  <select
                    value={formData.currency}
                    onChange={(e) => setFormData({ ...formData, currency: e.target.value })}
                    className="w-full bg-slate-50 border border-sky-100 rounded-xl px-3 py-2 text-slate-800 focus:outline-none focus:border-sky-500 focus:bg-white"
                  >
                    <option value="TWD">TWD 新台幣</option>
                    <option value={currentTrip?.currency || 'JPY'}>{currentTrip?.currency || 'JPY'} 當地外幣</option>
                  </select>
                </div>
                <div className="col-span-2">
                  <label className="block text-slate-600 mb-1 font-semibold">原幣支付金額</label>
                  <input
                    type="number"
                    step="any"
                    required
                    placeholder="例如 12000"
                    value={formData.origAmount}
                    onChange={(e) => setFormData({ ...formData, origAmount: e.target.value })}
                    className="w-full bg-slate-50 border border-sky-100 rounded-xl px-3 py-2 text-slate-800 focus:outline-none focus:border-sky-500 focus:bg-white"
                  />
                </div>
              </div>

              {/* 即時折合台幣提示 */}
              {formData.origAmount && formData.currency !== 'TWD' && (
                <div className="p-2.5 rounded-xl bg-amber-50 border border-amber-200 text-amber-800 flex items-center justify-between">
                  <span>依加權匯率 ({exchangeStats.avgRate.toFixed(4)}) 折合：</span>
                  <span className="font-bold text-sm">
                    ≈ ${Math.round(Number(formData.origAmount) * exchangeStats.avgRate).toLocaleString()} TWD
                  </span>
                </div>
              )}

              {/* 支付方式 (星展信用卡 vs 外幣現金) */}
              <div className="space-y-2 pt-1 border-t border-sky-100">
                <label className="block text-slate-600 font-semibold">支付方式</label>
                <div className="grid grid-cols-2 gap-3">
                  <button
                    type="button"
                    onClick={() => setFormData({ ...formData, payMethod: 'card' })}
                    className={`p-2.5 rounded-xl border flex items-center justify-center space-x-2 transition ${
                      formData.payMethod === 'card'
                        ? 'bg-sky-50 border-sky-500 text-sky-800 font-semibold shadow-2xs'
                        : 'bg-slate-50 border-sky-100 text-slate-500'
                    }`}
                  >
                    <CreditCard className="w-4 h-4 text-sky-600" />
                    <span>刷星展信用卡</span>
                  </button>

                  <button
                    type="button"
                    onClick={() => setFormData({ ...formData, payMethod: 'cash' })}
                    className={`p-2.5 rounded-xl border flex items-center justify-center space-x-2 transition ${
                      formData.payMethod === 'cash'
                        ? 'bg-amber-50 border-amber-400 text-amber-800 font-semibold shadow-2xs'
                        : 'bg-slate-50 border-sky-100 text-slate-500'
                    }`}
                  >
                    <Wallet className="w-4 h-4 text-amber-600" />
                    <span>外幣現金現鈔</span>
                  </button>
                </div>

                {formData.payMethod === 'card' && (
                  <div className="mt-2">
                    <label className="block text-slate-600 mb-1 font-medium">使用哪張星展信用卡？</label>
                    <select
                      value={formData.cardId}
                      onChange={(e) => setFormData({ ...formData, cardId: e.target.value })}
                      className="w-full bg-slate-50 border border-sky-100 rounded-xl px-3 py-2 text-slate-800 focus:outline-none focus:border-sky-500 focus:bg-white"
                    >
                      {cards.map((c) => (
                        <option key={c.id} value={c.id}>
                          {c.name} (海外回饋 {c.rate}%, 手續費 {c.fee}%)
                        </option>
                      ))}
                    </select>
                  </div>
                )}
              </div>

              {/* --- 核心分攤設定 --- */}
              <div className="pt-2 border-t border-sky-100 space-y-3">
                <div className="grid grid-cols-2 gap-3">
                  <div>
                    <label className="block text-slate-600 mb-1 font-semibold">先付款人是誰？</label>
                    <select
                      value={formData.payer}
                      onChange={(e) => setFormData({ ...formData, payer: e.target.value })}
                      className="w-full bg-slate-50 border border-sky-100 rounded-xl px-3 py-2 text-slate-800 focus:outline-none focus:border-sky-500 focus:bg-white"
                    >
                      {currentTrip?.companions?.map((c) => (
                        <option key={c} value={c}>{c}</option>
                      ))}
                    </select>
                  </div>

                  <div>
                    <label className="block text-slate-600 mb-1 font-semibold">分攤模式</label>
                    <select
                      value={formData.splitType}
                      onChange={(e) => setFormData({ ...formData, splitType: e.target.value })}
                      className="w-full bg-slate-50 border border-sky-100 rounded-xl px-3 py-2 text-slate-800 focus:outline-none focus:border-sky-500 focus:bg-white"
                    >
                      <option value="selected_even">成員多選平分 (有吃有買才打勾)</option>
                      <option value="self">個人全自費 (只有付款人)</option>
                      <option value="custom_amount">自訂每人金額 (各自點不同)</option>
                      <option value="single_reimburse">專屬單人代墊 (幫某人代買)</option>
                    </select>
                  </div>
                </div>

                {/* 模式 A：多選成員打勾平分 */}
                {formData.splitType === 'selected_even' && (
                  <div className="p-3 bg-sky-50/60 border border-sky-100 rounded-xl">
                    <span className="block text-slate-700 font-semibold mb-2">
                      請勾選參與此消費的旅伴名單（系統將總額平分給有打勾的人）：
                    </span>
                    <div className="grid grid-cols-2 gap-2">
                      {currentTrip?.companions?.map((companion) => {
                        const isChecked = formData.involvedCompanions?.includes(companion);
                        return (
                          <label
                            key={companion}
                            className={`flex items-center space-x-2 p-2 rounded-lg border cursor-pointer transition ${
                              isChecked
                                ? 'bg-white border-sky-500 text-sky-800 font-semibold shadow-2xs'
                                : 'bg-white/70 border-sky-100 text-slate-500'
                            }`}
                          >
                            <input
                              type="checkbox"
                              checked={isChecked}
                              onChange={() => {
                                const current = formData.involvedCompanions || [];
                                const updated = isChecked
                                  ? current.filter(c => c !== companion)
                                  : [...current, companion];
                                setFormData({ ...formData, involvedCompanions: updated });
                              }}
                              className="rounded border-sky-300 text-sky-600 focus:ring-0"
                            />
                            <span>{companion}</span>
                          </label>
                        );
                      })}
                    </div>
                  </div>
                )}

                {/* 模式 B：自訂每人金額 */}
                {formData.splitType === 'custom_amount' && (
                  <div className="p-3 bg-sky-50/60 border border-sky-100 rounded-xl space-y-2">
                    <span className="block text-slate-700 font-semibold">請輸入每位旅伴各自負擔的原幣金額：</span>
                    {currentTrip?.companions?.map((companion) => (
                      <div key={companion} className="flex items-center space-x-2">
                        <span className="w-24 text-slate-700 font-medium">{companion}</span>
                        <input
                          type="number"
                          placeholder="0"
                          value={formData.customAmounts?.[companion] || ''}
                          onChange={(e) => {
                            setFormData({
                              ...formData,
                              customAmounts: {
                                ...formData.customAmounts,
                                [companion]: parseFloat(e.target.value) || 0
                              }
                            });
                          }}
                          className="flex-1 bg-white border border-sky-200 rounded-lg px-2.5 py-1 text-slate-800 focus:outline-none focus:border-sky-500"
                        />
                        <span className="text-slate-400">{formData.currency}</span>
                      </div>
                    ))}
                  </div>
                )}

                {/* 模式 C：單人專屬代墊 */}
                {formData.splitType === 'single_reimburse' && (
                  <div className="p-3 bg-sky-50/60 border border-sky-100 rounded-xl">
                    <label className="block text-slate-700 font-semibold mb-1.5">這筆消費是專門替誰代墊代買的？</label>
                    <select
                      value={formData.targetCompanion}
                      onChange={(e) => setFormData({ ...formData, targetCompanion: e.target.value })}
                      className="w-full bg-white border border-sky-200 rounded-lg px-3 py-1.5 text-slate-800 focus:outline-none focus:border-sky-500"
                    >
                      {currentTrip?.companions?.map((c) => (
                        <option key={c} value={c}>{c}</option>
                      ))}
                    </select>
                    <p className="text-[11px] text-slate-500 mt-2">
                      付款人墊付此筆全額，後續將全數由【{formData.targetCompanion || '指定旅伴'}】歸還。
                    </p>
                  </div>
                )}
              </div>

              {/* 備註說明 */}
              <div>
                <label className="block text-slate-600 mb-1 font-semibold">備註說明 (選填)</label>
                <input
                  type="text"
                  placeholder="例如：特定門票、退稅單留存"
                  value={formData.notes}
                  onChange={(e) => setFormData({ ...formData, notes: e.target.value })}
                  className="w-full bg-slate-50 border border-sky-100 rounded-xl px-3 py-2 text-slate-800 focus:outline-none focus:border-sky-500 focus:bg-white"
                />
              </div>

              <div className="pt-3 flex items-center justify-end space-x-3 border-t border-sky-100">
                <button
                  type="button"
                  onClick={() => setIsExpenseModalOpen(false)}
                  className="px-4 py-2 rounded-xl text-slate-500 hover:text-slate-800 font-medium"
                >
                  取消
                </button>
                <button
                  type="submit"
                  className="px-6 py-2 bg-gradient-to-r from-sky-500 to-blue-600 hover:from-sky-600 hover:to-blue-700 text-white rounded-xl font-semibold shadow-sm shadow-sky-200 transition"
                >
                  確認儲存
                </button>
              </div>
            </form>
          </div>
        </div>
      )}

      {/* --- MODAL 2: 旅伴成員名單管理 --- */}
      {isCompanionModalOpen && currentTrip && (
        <div className="fixed inset-0 z-50 flex items-center justify-center p-4 bg-slate-900/40 backdrop-blur-sm animate-in fade-in duration-150">
          <div className="bg-white border border-sky-100 rounded-3xl max-w-md w-full p-6 shadow-2xl">
            <div className="flex items-center justify-between pb-3 border-b border-sky-100">
              <h3 className="text-base font-bold text-slate-800 flex items-center">
                <Users className="w-4 h-4 mr-2 text-sky-600" />
                管理旅伴名單【{currentTrip.name}】
              </h3>
              <button onClick={() => setIsCompanionModalOpen(false)} className="text-slate-400 hover:text-slate-700">✕</button>
            </div>

            <div className="mt-4 space-y-3 text-xs">
              <form onSubmit={handleAddCompanion} className="flex gap-2">
                <input
                  type="text"
                  required
                  placeholder="輸入旅伴姓名 (如 小花、大明)..."
                  value={newCompanionName}
                  onChange={(e) => setNewCompanionName(e.target.value)}
                  className="flex-1 bg-slate-50 border border-sky-100 rounded-xl px-3 py-2 text-slate-800 focus:outline-none focus:border-sky-500 focus:bg-white"
                />
                <button
                  type="submit"
                  className="px-4 py-2 bg-gradient-to-r from-sky-500 to-blue-600 hover:from-sky-600 hover:to-blue-700 text-white rounded-xl font-semibold shadow-2xs"
                >
                  新增成員
                </button>
              </form>

              <div className="pt-2">
                <span className="text-slate-500 block mb-2 font-medium">現有同行旅伴：</span>
                <div className="space-y-2 max-h-56 overflow-y-auto">
                  {currentTrip.companions.map((name) => (
                    <div
                      key={name}
                      className="flex items-center justify-between p-2.5 bg-sky-50/50 border border-sky-100 rounded-xl"
                    >
                      <span className="font-semibold text-slate-800">{name} {name === '我' && '(自己)'}</span>
                      {name !== '我' && (
                        <button
                          onClick={() => handleRemoveCompanion(name)}
                          className="text-slate-400 hover:text-rose-500 p-1"
                        >
                          <Trash2 className="w-3.5 h-3.5" />
                        </button>
                      )}
                    </div>
                  ))}
                </div>
              </div>

              <div className="pt-3 flex justify-end">
                <button
                  onClick={() => setIsCompanionModalOpen(false)}
                  className="px-5 py-2 bg-slate-100 hover:bg-slate-200 text-slate-700 rounded-xl font-semibold"
                >
                  完成關閉
                </button>
              </div>
            </div>
          </div>
        </div>
      )}

      {/* --- MODAL 3: 新增換匯記錄 --- */}
      {isExchangeModalOpen && currentTrip && (
        <div className="fixed inset-0 z-50 flex items-center justify-center p-4 bg-slate-900/40 backdrop-blur-sm animate-in fade-in duration-150">
          <div className="bg-white border border-sky-100 rounded-3xl max-w-md w-full p-6 shadow-2xl">
            <div className="flex items-center justify-between pb-3 border-b border-sky-100">
              <h3 className="text-base font-bold text-slate-800 flex items-center">
                <ArrowRightLeft className="w-4 h-4 mr-2 text-amber-500" />
                新增換匯紀錄 ({currentTrip.currency})
              </h3>
              <button onClick={() => setIsExchangeModalOpen(false)} className="text-slate-400 hover:text-slate-700">✕</button>
            </div>

            <form onSubmit={handleAddExchange} className="mt-4 space-y-3 text-xs">
              <div>
                <label className="block text-slate-600 mb-1 font-semibold">換匯日期</label>
                <input
                  type="date"
                  required
                  value={newExchange.date}
                  onChange={(e) => setNewExchange({ ...newExchange, date: e.target.value })}
                  className="w-full bg-slate-50 border border-sky-100 rounded-xl px-3 py-2 text-slate-800 focus:outline-none focus:border-sky-500 focus:bg-white"
                />
              </div>

              <div>
                <label className="block text-slate-600 mb-1 font-semibold">支付台幣總金額 (TWD)</label>
                <input
                  type="number"
                  required
                  placeholder="例如 20000"
                  value={newExchange.twdAmount}
                  onChange={(e) => setNewExchange({ ...newExchange, twdAmount: e.target.value })}
                  className="w-full bg-slate-50 border border-sky-100 rounded-xl px-3 py-2 text-slate-800 focus:outline-none focus:border-sky-500 focus:bg-white"
                />
              </div>

              <div>
                <label className="block text-slate-600 mb-1 font-semibold">實際換得外幣 ({currentTrip.currency})</label>
                <input
                  type="number"
                  required
                  placeholder="例如 92000"
                  value={newExchange.foreignAmount}
                  onChange={(e) => setNewExchange({ ...newExchange, foreignAmount: e.target.value })}
                  className="w-full bg-slate-50 border border-sky-100 rounded-xl px-3 py-2 text-slate-800 focus:outline-none focus:border-sky-500 focus:bg-white"
                />
              </div>

              {newExchange.twdAmount && newExchange.foreignAmount && Number(newExchange.foreignAmount) > 0 && (
                <div className="text-amber-800 text-xs bg-amber-50 p-2.5 rounded-xl border border-amber-200">
                  實質匯率：<strong>{(Number(newExchange.twdAmount) / Number(newExchange.foreignAmount)).toFixed(4)}</strong> TWD / {currentTrip.currency}
                </div>
              )}

              <div>
                <label className="block text-slate-600 mb-1 font-semibold">換匯管道與備註</label>
                <input
                  type="text"
                  placeholder="例如：星展 Card+ 線上結匯、台銀臨櫃換現鈔"
                  value={newExchange.channel}
                  onChange={(e) => setNewExchange({ ...newExchange, channel: e.target.value })}
                  className="w-full bg-slate-50 border border-sky-100 rounded-xl px-3 py-2 text-slate-800 focus:outline-none focus:border-sky-500 focus:bg-white"
                />
              </div>

              <div className="pt-3 flex justify-end space-x-2">
                <button
                  type="button"
                  onClick={() => setIsExchangeModalOpen(false)}
                  className="px-4 py-2 text-slate-500 hover:text-slate-800 font-medium"
                >
                  取消
                </button>
                <button
                  type="submit"
                  className="px-5 py-2 bg-gradient-to-r from-amber-500 to-amber-600 hover:from-amber-600 hover:to-amber-700 text-white rounded-xl font-semibold shadow-2xs"
                >
                  確認新增
                </button>
              </div>
            </form>
          </div>
        </div>
      )}

      {/* --- MODAL 4: 規劃新旅程 --- */}
      {isTripModalOpen && (
        <div className="fixed inset-0 z-50 flex items-center justify-center p-4 bg-slate-900/40 backdrop-blur-sm animate-in fade-in duration-150">
          <div className="bg-white border border-sky-100 rounded-3xl max-w-md w-full p-6 shadow-2xl">
            <div className="flex items-center justify-between pb-3 border-b border-sky-100">
              <h3 className="text-base font-bold text-slate-800 flex items-center">
                <MapPin className="w-4 h-4 mr-2 text-sky-600" />
                規劃並建立新旅程
              </h3>
              <button onClick={() => setIsTripModalOpen(false)} className="text-slate-400 hover:text-slate-700">✕</button>
            </div>

            <form onSubmit={handleCreateTrip} className="mt-4 space-y-3 text-xs">
              <div>
                <label className="block text-slate-600 mb-1 font-semibold">旅程名稱與目的地</label>
                <input
                  type="text"
                  required
                  placeholder="例如：2027/04 日本京都賞櫻"
                  value={newTripData.name}
                  onChange={(e) => setNewTripData({ ...newTripData, name: e.target.value })}
                  className="w-full bg-slate-50 border border-sky-100 rounded-xl px-3 py-2 text-slate-800 focus:outline-none focus:border-sky-500 focus:bg-white"
                />
              </div>

              <div className="grid grid-cols-2 gap-3">
                <div>
                  <label className="block text-slate-600 mb-1 font-semibold">出發日期</label>
                  <input
                    type="date"
                    required
                    value={newTripData.startDate}
                    onChange={(e) => setNewTripData({ ...newTripData, startDate: e.target.value })}
                    className="w-full bg-slate-50 border border-sky-100 rounded-xl px-3 py-2 text-slate-800 focus:outline-none focus:border-sky-500 focus:bg-white"
                  />
                </div>
                <div>
                  <label className="block text-slate-600 mb-1 font-semibold">返程日期</label>
                  <input
                    type="date"
                    required
                    value={newTripData.endDate}
                    onChange={(e) => setNewTripData({ ...newTripData, endDate: e.target.value })}
                    className="w-full bg-slate-50 border border-sky-100 rounded-xl px-3 py-2 text-slate-800 focus:outline-none focus:border-sky-500 focus:bg-white"
                  />
                </div>
              </div>

              <div className="grid grid-cols-2 gap-3">
                <div>
                  <label className="block text-slate-600 mb-1 font-semibold">當地外幣代碼</label>
                  <input
                    type="text"
                    required
                    placeholder="JPY, THB, EUR, KRW..."
                    value={newTripData.currency}
                    onChange={(e) => setNewTripData({ ...newTripData, currency: e.target.value.toUpperCase() })}
                    className="w-full bg-slate-50 border border-sky-100 rounded-xl px-3 py-2 text-slate-800 focus:outline-none focus:border-sky-500 focus:bg-white"
                  />
                </div>
                <div>
                  <label className="block text-slate-600 mb-1 font-semibold">貨幣符號</label>
                  <input
                    type="text"
                    placeholder="¥, ฿, €, ₩..."
                    value={newTripData.currencySymbol}
                    onChange={(e) => setNewTripData({ ...newTripData, currencySymbol: e.target.value })}
                    className="w-full bg-slate-50 border border-sky-100 rounded-xl px-3 py-2 text-slate-800 focus:outline-none focus:border-sky-500 focus:bg-white"
                  />
                </div>
              </div>

              <div>
                <label className="block text-slate-600 mb-1 font-semibold">目標總預算 (TWD)</label>
                <input
                  type="number"
                  placeholder="例如 65000"
                  value={newTripData.targetBudgetTWD}
                  onChange={(e) => setNewTripData({ ...newTripData, targetBudgetTWD: e.target.value })}
                  className="w-full bg-slate-50 border border-sky-100 rounded-xl px-3 py-2 text-slate-800 focus:outline-none focus:border-sky-500 focus:bg-white"
                />
              </div>

              <div>
                <label className="block text-slate-600 mb-1 font-semibold">同行旅伴名單 (用逗號隔開)</label>
                <input
                  type="text"
                  placeholder="我, 佳諭, 逸軒, 傅資深經理"
                  value={newTripData.companions}
                  onChange={(e) => setNewTripData({ ...newTripData, companions: e.target.value })}
                  className="w-full bg-slate-50 border border-sky-100 rounded-xl px-3 py-2 text-slate-800 focus:outline-none focus:border-sky-500 focus:bg-white"
                />
              </div>

              <div className="pt-3 flex justify-end space-x-2">
                <button
                  type="button"
                  onClick={() => setIsTripModalOpen(false)}
                  className="px-4 py-2 text-slate-500 hover:text-slate-800 font-medium"
                >
                  取消
                </button>
                <button
                  type="submit"
                  className="px-5 py-2 bg-gradient-to-r from-sky-500 to-blue-600 hover:from-sky-600 hover:to-blue-700 text-white rounded-xl font-semibold shadow-sm shadow-sky-200 transition"
                >
                  建立旅程
                </button>
              </div>
            </form>
          </div>
        </div>
      )}

      {/* --- MODAL 5: 新增自訂星展信用卡 --- */}
      {isCardModalOpen && (
        <div className="fixed inset-0 z-50 flex items-center justify-center p-4 bg-slate-900/40 backdrop-blur-sm animate-in fade-in duration-150">
          <div className="bg-white border border-sky-100 rounded-3xl max-w-md w-full p-6 shadow-2xl">
            <div className="flex items-center justify-between pb-3 border-b border-sky-100">
              <h3 className="text-base font-bold text-slate-800 flex items-center">
                <CreditCard className="w-4 h-4 mr-2 text-sky-600" />
                新增星展信用卡
              </h3>
              <button onClick={() => setIsCardModalOpen(false)} className="text-slate-400 hover:text-slate-700">✕</button>
            </div>

            <form onSubmit={handleAddCard} className="mt-4 space-y-3 text-xs">
              <div>
                <label className="block text-slate-600 mb-1 font-semibold">卡片名稱</label>
                <input
                  type="text"
                  required
                  placeholder="例如：星展 饗樂生活卡、星展 頂級卡"
                  value={newCard.name}
                  onChange={(e) => setNewCard({ ...newCard, name: e.target.value })}
                  className="w-full bg-slate-50 border border-sky-100 rounded-xl px-3 py-2 text-slate-800 focus:outline-none focus:border-sky-500 focus:bg-white"
                />
              </div>

              <div className="grid grid-cols-2 gap-3">
                <div>
                  <label className="block text-slate-600 mb-1 font-semibold">海外回饋率 (%)</label>
                  <input
                    type="number"
                    step="0.1"
                    required
                    placeholder="3.0"
                    value={newCard.rate}
                    onChange={(e) => setNewCard({ ...newCard, rate: e.target.value })}
                    className="w-full bg-slate-50 border border-sky-100 rounded-xl px-3 py-2 text-slate-800 focus:outline-none focus:border-sky-500 focus:bg-white"
                  />
                </div>
                <div>
                  <label className="block text-slate-600 mb-1 font-semibold">海外手續費 (%)</label>
                  <input
                    type="number"
                    step="0.1"
                    required
                    placeholder="1.5"
                    value={newCard.fee}
                    onChange={(e) => setNewCard({ ...newCard, fee: e.target.value })}
                    className="w-full bg-slate-50 border border-sky-100 rounded-xl px-3 py-2 text-slate-800 focus:outline-none focus:border-sky-500 focus:bg-white"
                  />
                </div>
              </div>

              <div>
                <label className="block text-slate-600 mb-1 font-semibold">備註說明 (如哩程換算或特約店家)</label>
                <input
                  type="text"
                  placeholder="例如：指定旅遊通路加碼或免手續費"
                  value={newCard.notes}
                  onChange={(e) => setNewCard({ ...newCard, notes: e.target.value })}
                  className="w-full bg-slate-50 border border-sky-100 rounded-xl px-3 py-2 text-slate-800 focus:outline-none focus:border-sky-500 focus:bg-white"
                />
              </div>

              <div className="pt-3 flex justify-end space-x-2">
                <button
                  type="button"
                  onClick={() => setIsCardModalOpen(false)}
                  className="px-4 py-2 text-slate-500 hover:text-slate-800 font-medium"
                >
                  取消
                </button>
                <button
                  type="submit"
                  className="px-5 py-2 bg-gradient-to-r from-sky-500 to-blue-600 hover:from-sky-600 hover:to-blue-700 text-white rounded-xl font-semibold shadow-xs"
                >
                  儲存卡片
                </button>
              </div>
            </form>
          </div>
        </div>
      )}
    </div>
  );
}
