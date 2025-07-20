<!DOCTYPE html>
<html lang="fa" dir="rtl">
<head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>دزدگیر اماکن</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <meta name="theme-color" content="#0891b2" />
    <meta name="description" content="یک ابزار تحت وب برای کنترل سیستم امنیتی خانه (دزدگیر) از طریق ارسال دستورات پیامکی. کاربران می توانند کلیدها و دستورات را سفارشی سازی کرده و تنظیمات را برای استفاده های بعدی ذخیره کنند.">
    
    <style>
        body {
            -webkit-font-smoothing: antialiased;
            -moz-osx-font-smoothing: grayscale;
        }
    </style>

    <!-- React and Babel for running JSX in the browser -->
    <script src="https://unpkg.com/react@18/umd/react.development.js"></script>
    <script src="https://unpkg.com/react-dom@18/umd/react-dom.development.js"></script>
    <script src="https://unpkg.com/@babel/standalone/babel.min.js"></script>

<script type="importmap">
{
  "imports": {
    "react": "https://esm.sh/react@^19.1.0",
    "react-dom/": "https://esm.sh/react-dom@^19.1.0/",
    "react/": "https://esm.sh/react@^19.1.0/"
  }
}
</script>
<link rel="stylesheet" href="/index.css">
</head>
<body class="bg-gray-900">
    <div id="root"></div>

    <script type="text/babel">
        const { useState, useEffect, useCallback, useRef } = React;

        // --- from types.ts ---
        /*
        interface KeyConfig {
            id: number;
            label: string;
            onCommand: string;
            offCommand: string;
        }

        interface AlarmConfig {
            phoneNumber: string;
            keys: KeyConfig[];
            sirenCommand: string;
            passwordHash: string | null;
        }
        */

        // --- from hooks/useAlarmConfig.ts ---
        const useAlarmConfig = () => {
            const CONFIG_KEY = 'alarmConfigV2';

            const getDefaultConfig = () => ({
                phoneNumber: '',
                keys: Array.from({ length: 6 }, (_, i) => ({
                    id: i + 1,
                    label: `کلید ${i + 1}`,
                    onCommand: `ON${i + 1}`,
                    offCommand: `OFF${i + 1}`,
                })),
                sirenCommand: 'SIREN_OFF',
                passwordHash: null,
            });

            const loadConfig = () => {
                try {
                    const savedConfig = localStorage.getItem(CONFIG_KEY);
                    if (savedConfig) {
                        const parsedConfig = JSON.parse(savedConfig);
                        if (parsedConfig.phoneNumber !== undefined && parsedConfig.keys && parsedConfig.sirenCommand) {
                            const validatedKeys = parsedConfig.keys.map((key, index) => ({
                                id: key.id || index + 1,
                                label: key.label || `کلید ${index + 1}`,
                                onCommand: key.onCommand || `ON${index + 1}`,
                                offCommand: key.offCommand || `OFF${index + 1}`,
                            }));
                            return { ...getDefaultConfig(), ...parsedConfig, keys: validatedKeys };
                        }
                    }
                } catch (error) {
                    console.error("Failed to load or parse config from localStorage:", error);
                }
                return getDefaultConfig();
            };
            
            const hashPassword = async (password) => {
                const encoder = new TextEncoder();
                const data = encoder.encode(password);
                const hashBuffer = await crypto.subtle.digest('SHA-256', data);
                const hashArray = Array.from(new Uint8Array(hashBuffer));
                return hashArray.map(b => b.toString(16).padStart(2, '0')).join('');
            };

            const [config, setConfig] = useState(loadConfig());
            const [isEditing, setIsEditing] = useState(false);

            useEffect(() => {
                try {
                    localStorage.setItem(CONFIG_KEY, JSON.stringify(config));
                } catch (error) {
                    console.error("Failed to save config to localStorage:", error);
                }
            }, [config]);

            const updatePhoneNumber = useCallback((phoneNumber) => {
                setConfig(prevConfig => ({ ...prevConfig, phoneNumber }));
            }, []);

            const updateKey = useCallback((id, field, value) => {
                setConfig(prevConfig => ({
                    ...prevConfig,
                    keys: prevConfig.keys.map(key =>
                        key.id === id ? { ...key, [field]: value } : key
                    ),
                }));
            }, []);

            const updateSirenCommand = useCallback((command) => {
                setConfig(prevConfig => ({ ...prevConfig, sirenCommand: command }));
            }, []);

            const toggleEditMode = useCallback(() => {
                setIsEditing(prev => !prev);
            }, []);

            const setPassword = useCallback(async (password) => {
                const passwordHash = await hashPassword(password);
                setConfig(prevConfig => ({ ...prevConfig, passwordHash }));
            }, []);

            const login = useCallback(async (password) => {
                if (!config.passwordHash) return false;
                const inputHash = await hashPassword(password);
                return inputHash === config.passwordHash;
            }, [config.passwordHash]);

            const addKey = useCallback(() => {
                const newKey = {
                    id: Date.now(), // Use timestamp for a unique ID
                    label: 'کلید جدید',
                    onCommand: '',
                    offCommand: '',
                };
                setConfig(prevConfig => ({
                    ...prevConfig,
                    keys: [...prevConfig.keys, newKey],
                }));
            }, []);

            const removeKey = useCallback((id) => {
                setConfig(prevConfig => ({
                    ...prevConfig,
                    keys: prevConfig.keys.filter(key => key.id !== id),
                }));
            }, []);

            return {
                config,
                isEditing,
                updatePhoneNumber,
                updateKey,
                updateSirenCommand,
                toggleEditMode,
                setPassword,
                login,
                addKey,
                removeKey,
            };
        };


        // --- from components/Header.tsx ---
        const Header = () => (
            <header className="text-center mb-8 flex flex-col items-center gap-4">
                <svg xmlns="http://www.w3.org/2000/svg" className="h-16 w-16 text-cyan-400" viewBox="0 0 20 20" fill="currentColor">
                    <path d="M10.707 2.293a1 1 0 00-1.414 0l-7 7a1 1 0 001.414 1.414L4 10.414V17a1 1 0 001 1h2a1 1 0 001-1v-2a1 1 0 011-1h2a1 1 0 011 1v2a1 1 0 001 1h2a1 1 0 001-1v-6.586l.293.293a1 1 0 001.414-1.414l-7-7z" />
                </svg>
                <h1 className="text-4xl sm:text-5xl font-bold text-transparent bg-clip-text bg-gradient-to-r from-cyan-400 to-blue-500">
                    دزدگیر اماکن
                </h1>
                <p className="text-gray-400">پنل کنترل از راه دور با پیامک</p>
            </header>
        );

        // --- from components/PhoneNumberInput.tsx ---
        const PhoneNumberInput = ({ phoneNumber, onUpdate }) => (
            <div className="flex-grow w-full">
                <label htmlFor="phoneNumber" className="block text-sm font-medium text-gray-300 mb-2">
                    شماره تلفن دزدگیر
                </label>
                <input 
                    type="tel" 
                    id="phoneNumber" 
                    value={phoneNumber}
                    onChange={(e) => onUpdate(e.target.value)}
                    placeholder="مثال: 09123456789" 
                    className="w-full bg-gray-700 text-white border border-gray-600 rounded-md p-3 focus:ring-2 focus:ring-cyan-500 focus:border-cyan-500 transition text-left" 
                    dir="ltr" 
                />
            </div>
        );

        // --- from components/EditButton.tsx ---
        const EditButton = ({ isEditing, onToggle }) => (
            <div className="w-full sm:w-auto">
                <button 
                    onClick={onToggle}
                    className="w-full sm:w-auto mt-auto px-6 py-3 bg-gradient-to-r from-purple-500 to-indigo-600 hover:from-purple-600 hover:to-indigo-700 rounded-md transition-all duration-300 transform hover:scale-105 shadow-lg flex items-center justify-center gap-2"
                >
                    <svg xmlns="http://www.w3.org/2000/svg" className="h-5 w-5" viewBox="0 0 20 20" fill="currentColor">
                        <path d="M17.414 2.586a2 2 0 00-2.828 0L7 10.172V13h2.828l7.586-7.586a2 2 0 000-2.828z" />
                        <path fillRule="evenodd" d="M2 6a2 2 0 012-2h4a1 1 0 010 2H4v10h10v-4a1 1 0 112 0v4a2 2 0 01-2 2H4a2 2 0 01-2-2V6z" clipRule="evenodd" />
                    </svg>
                    <span>
                        {isEditing ? 'ذخیره و پایان ویرایش' : 'ویرایش کلیدها'}
                    </span>
                </button>
            </div>
        );

        // --- from components/LogoutButton.tsx ---
        const LogoutButton = ({ onLogout }) => (
            <div className="w-full sm:w-auto">
                <button 
                    onClick={onLogout}
                    title="خروج"
                    className="w-full sm:w-auto mt-auto p-3 bg-gradient-to-r from-red-500 to-pink-600 hover:from-red-600 hover:to-pink-700 rounded-md transition-all duration-300 transform hover:scale-105 shadow-lg flex items-center justify-center"
                >
                    <svg xmlns="http://www.w3.org/2000/svg" className="h-5 w-5" viewBox="0 0 20 20" fill="currentColor">
                        <path fillRule="evenodd" d="M3 3a1 1 0 00-1 1v12a1 1 0 102 0V4a1 1 0 00-1-1zm10.293 9.293a1 1 0 001.414 1.414l3-3a1 1 0 000-1.414l-3-3a1 1 0 10-1.414 1.414L14.586 9H7a1 1 0 100 2h7.586l-1.293 1.293z" clipRule="evenodd" />
                    </svg>
                </button>
            </div>
        );

        // --- from components/KeyControl.tsx ---
        const KeyControl = ({ keyData, isEditing, onUpdate, onSendCommand, onRemove }) => {
            const handleRemove = () => {
                if (window.confirm(`آیا از حذف کلید "${keyData.label}" مطمئن هستید؟ این عمل غیرقابل بازگشت است.`)) {
                    onRemove(keyData.id);
                }
            };

            return (
                <div className="bg-gray-800 rounded-xl p-4 border border-gray-700 shadow-lg flex flex-col gap-4 transition-all duration-300">
                    {isEditing ? (
                         <div className="flex items-center gap-2">
                            <input
                                type="text"
                                value={keyData.label}
                                onChange={(e) => onUpdate('label', e.target.value)}
                                className="key-input w-full bg-gray-700 text-white font-bold text-lg text-center border-b-2 border-purple-500 rounded-t-md p-2 focus:outline-none focus:ring-2 focus:ring-purple-500"
                            />
                            <button
                                onClick={handleRemove}
                                title="حذف کلید"
                                className="p-2 bg-red-600/50 hover:bg-red-600 rounded-md text-white transition-colors duration-200 flex-shrink-0"
                            >
                                <svg xmlns="http://www.w3.org/2000/svg" className="h-5 w-5" viewBox="0 0 20 20" fill="currentColor">
                                    <path fillRule="evenodd" d="M9 2a1 1 0 00-.894.553L7.382 4H4a1 1 0 000 2v10a2 2 0 002 2h8a2 2 0 002-2V6a1 1 0 100-2h-3.382l-.724-1.447A1 1 0 0011 2H9zM7 8a1 1 0 012 0v6a1 1 0 11-2 0V8zm4 0a1 1 0 012 0v6a1 1 0 11-2 0V8z" clipRule="evenodd" />
                                </svg>
                            </button>
                        </div>
                    ) : (
                        <div>
                            <h3 className="text-lg font-bold text-center text-gray-200 py-2">{keyData.label}</h3>
                        </div>
                    )}
                   
                    {isEditing && (
                        <div className="flex flex-col gap-3">
                            <div>
                                <label className="block text-xs font-medium text-gray-400 mb-1">دستور روشن</label>
                                <input
                                    type="text"
                                    value={keyData.onCommand}
                                    onChange={(e) => onUpdate('onCommand', e.target.value)}
                                    className="key-input w-full bg-gray-900 text-white border border-gray-600 rounded-md p-2 focus:ring-1 focus:ring-green-500 focus:border-green-500 transition text-left text-sm"
                                    dir="ltr"
                                />
                            </div>
                            <div>
                                <label className="block text-xs font-medium text-gray-400 mb-1">دستور خاموش</label>
                                <input
                                    type="text"
                                    value={keyData.offCommand}
                                    onChange={(e) => onUpdate('offCommand', e.target.value)}
                                    className="key-input w-full bg-gray-900 text-white border border-gray-600 rounded-md p-2 focus:ring-1 focus:ring-red-500 focus:border-red-500 transition text-left text-sm"
                                    dir="ltr"
                                />
                            </div>
                        </div>
                    )}
                    
                    <div className={`grid grid-cols-2 gap-3 ${isEditing ? 'mt-2' : 'mt-auto'}`}>
                        <button 
                            onClick={() => onSendCommand(keyData.onCommand)}
                            className="w-full px-4 py-3 bg-green-600 hover:bg-green-700 text-white font-semibold rounded-md transition-all duration-300 transform hover:scale-105 shadow-md flex items-center justify-center gap-2"
                        >
                            <svg xmlns="http://www.w3.org/2000/svg" className="h-5 w-5" viewBox="0 0 20 20" fill="currentColor">
                              <path fillRule="evenodd" d="M10 18a8 8 0 100-16 8 8 0 000 16zm1-11a1 1 0 10-2 0v2H7a1 1 0 100 2h2v2a1 1 0 102 0v-2h2a1 1 0 100-2h-2V7z" clipRule="evenodd" />
                            </svg>
                            <span>روشن</span>
                        </button>
                        <button 
                            onClick={() => onSendCommand(keyData.offCommand)}
                            className="w-full px-4 py-3 bg-red-600 hover:bg-red-700 text-white font-semibold rounded-md transition-all duration-300 transform hover:scale-105 shadow-md flex items-center justify-center gap-2"
                        >
                            <svg xmlns="http://www.w3.org/2000/svg" className="h-5 w-5" viewBox="0 0 20 20" fill="currentColor">
                              <path fillRule="evenodd" d="M10 18a8 8 0 100-16 8 8 0 000 16zM7 9a1 1 0 000 2h6a1 1 0 100-2H7z" clipRule="evenodd" />
                            </svg>
                            <span>خاموش</span>
                        </button>
                    </div>
                </div>
            );
        };

        // --- from components/SirenControl.tsx ---
        const SirenControl = ({ sirenCommand, isEditing, onUpdate, onSendCommand }) => {
            return (
                <div className="bg-gray-800 rounded-xl p-6 border border-gray-700 shadow-lg">
                    <h3 className="text-xl font-bold text-amber-400 mb-4">کنترل آژیر</h3>
                    {isEditing && (
                        <div className="mb-4">
                            <label htmlFor="sirenCommand" className="block text-sm font-medium text-gray-300 mb-2">
                                دستور قطع آژیر
                            </label>
                            <input 
                                type="text" 
                                id="sirenCommand"
                                value={sirenCommand}
                                onChange={(e) => onUpdate(e.target.value)}
                                className="w-full bg-gray-700 text-white border border-gray-600 rounded-md p-3 focus:ring-2 focus:ring-amber-500 focus:border-amber-500 transition text-left" 
                                dir="ltr"
                            />
                        </div>
                    )}
                    <button 
                        onClick={() => onSendCommand(sirenCommand)} 
                        className="w-full px-6 py-4 bg-amber-500 hover:bg-amber-600 text-gray-900 font-bold rounded-md transition-all duration-300 transform hover:scale-105 shadow-lg flex items-center justify-center gap-2"
                    >
                        <svg xmlns="http://www.w3.org/2000/svg" className="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                            <path strokeLinecap="round" strokeLinejoin="round" strokeWidth="2" d="M15.536 8.464a5 5 0 010 7.072m2.828-9.9a9 9 0 010 12.728M5.858 5.858a3 3 0 10-4.242 4.243L12 21l10.385-10.893a3 3 0 10-4.242-4.243L12 10.172 5.858 5.858z" />
                            <path strokeLinecap="round" strokeLinejoin="round" strokeWidth="2" d="M18 9l-6 6-6-6" transform="rotate(-45 12 12)" />
                        </svg>
                        <span>قطع آژیر</span>
                    </button>
                </div>
            );
        };

        // --- from components/ManualAlarm.tsx ---
        const ManualAlarm = () => {
            const [isAlarmPlaying, setIsAlarmPlaying] = useState(false);
            const audioCtxRef = useRef(null);
            const oscillatorRef = useRef(null);

            const stopAlarm = useCallback(() => {
                if (audioCtxRef.current && audioCtxRef.current.state !== 'closed') {
                    audioCtxRef.current.close().then(() => {
                        audioCtxRef.current = null;
                        oscillatorRef.current = null;
                    });
                }
                setIsAlarmPlaying(false);
            }, []);

            const startAlarm = useCallback(() => {
                if (isAlarmPlaying || (audioCtxRef.current && audioCtxRef.current.state !== 'closed')) return;

                try {
                    const audioCtx = new (window.AudioContext)();
                    audioCtxRef.current = audioCtx;

                    const oscillator = audioCtx.createOscillator();
                    oscillator.type = 'square';
                    oscillator.frequency.setValueAtTime(800, audioCtx.currentTime); 
                    
                    const lfo = audioCtx.createOscillator();
                    lfo.type = 'sine';
                    lfo.frequency.setValueAtTime(2, audioCtx.currentTime);

                    const lfoGain = audioCtx.createGain();
                    lfoGain.gain.setValueAtTime(200, audioCtx.currentTime);

                    lfo.connect(lfoGain);
                    lfoGain.connect(oscillator.frequency);

                    const gainNode = audioCtx.createGain();
                    oscillator.connect(gainNode);
                    gainNode.connect(audioCtx.destination);

                    lfo.start();
                    oscillator.start();

                    oscillatorRef.current = oscillator;
                    setIsAlarmPlaying(true);

                } catch (e) {
                    console.error("Could not start audio:", e);
                    alert("مرورگر شما از پخش صدا پشتیبانی نمی‌کند یا دسترسی لازم داده نشده است.");
                    stopAlarm();
                }
            }, [isAlarmPlaying, stopAlarm]);
            
            const handleToggleAlarm = () => {
                if (isAlarmPlaying) {
                    stopAlarm();
                } else {
                    startAlarm();
                }
            };
            
            useEffect(() => {
              return () => {
                stopAlarm();
              };
            }, [stopAlarm]);
            
            return (
                <div className="bg-gray-800 rounded-xl p-6 border border-gray-700 shadow-lg mt-8">
                    <h3 className="text-xl font-bold text-red-400 mb-4">آژیر دستی اضطراری</h3>
                    <p className="text-gray-400 text-sm mb-4">
                       در مواقع اضطراری، آژیر را به صورت دستی از طریق بلندگوی دستگاه خود فعال کنید.
                    </p>
                    <button 
                        onClick={handleToggleAlarm} 
                        aria-pressed={isAlarmPlaying}
                        className={`w-full px-6 py-4 font-bold rounded-md transition-all duration-300 transform hover:scale-105 shadow-lg flex items-center justify-center gap-3
                            ${isAlarmPlaying 
                                ? 'bg-green-600 hover:bg-green-700 text-white animate-pulse'
                                : 'bg-red-600 hover:bg-red-700 text-white'}`
                        }
                    >
                        {isAlarmPlaying ? (
                            <>
                                <svg xmlns="http://www.w3.org/2000/svg" className="h-6 w-6" viewBox="0 0 20 20" fill="currentColor">
                                    <path fillRule="evenodd" d="M10 18a8 8 0 100-16 8 8 0 000 16zM8 7a1 1 0 00-1 1v4a1 1 0 102 0V8a1 1 0 00-1-1zm4 0a1 1 0 00-1 1v4a1 1 0 102 0V8a1 1 0 00-1-1z" clipRule="evenodd" />
                                </svg>
                                <span>توقف آژیر</span>
                            </>
                        ) : (
                            <>
                                <svg xmlns="http://www.w3.org/2000/svg" className="h-6 w-6" viewBox="0 0 20 20" fill="currentColor">
                                  <path d="M10 2a6 6 0 00-6 6v3.586l-.707.707A1 1 0 004 14h12a1 1 0 00.707-1.707L16 11.586V8a6 6 0 00-6-6zM10 16a2 2 0 100-4 2 2 0 000 4z" />
                                </svg>
                                <span>پخش آژیر</span>
                            </>
                        )}
                    </button>
                </div>
            );
        };

        // --- from components/Footer.tsx ---
        const Footer = () => (
            <footer className="text-center mt-12 py-4 border-t border-gray-800">
                <p className="text-gray-500 text-sm">
                    ساخته شده توسط امیر مهدی نوری
                </p>
            </footer>
        );

        // --- from components/LoginScreen.tsx ---
        const LoginScreen = ({ passwordIsSet, onLogin, onSetPassword }) => {
            const [password, setPassword] = useState('');
            const [confirmPassword, setConfirmPassword] = useState('');
            const [error, setError] = useState('');
            const [isLoading, setIsLoading] = useState(false);

            const handleSubmit = async (e) => {
                e.preventDefault();
                setError('');
                setIsLoading(true);

                if (passwordIsSet) {
                    const success = await onLogin(password);
                    if (!success) {
                        setError('رمز عبور وارد شده صحیح نیست.');
                    }
                } else {
                    if (password !== confirmPassword) {
                        setError('رمزهای عبور با یکدیگر مطابقت ندارند.');
                        setIsLoading(false);
                        return;
                    }
                    if(password.length < 4) {
                        setError('رمز عبور باید حداقل ۴ کاراکتر باشد.');
                        setIsLoading(false);
                        return;
                    }
                    await onSetPassword(password);
                }
                setIsLoading(false);
            };

            return (
                <div className="w-full max-w-md bg-gray-800/50 backdrop-blur-sm rounded-xl p-8 border border-gray-700 shadow-2xl">
                    <form onSubmit={handleSubmit} className="flex flex-col gap-6">
                        <div className="text-center">
                             <svg xmlns="http://www.w3.org/2000/svg" className="h-14 w-14 mx-auto text-cyan-400 mb-4" viewBox="0 0 20 20" fill="currentColor">
                                <path fillRule="evenodd" d="M10 1a4.5 4.5 0 00-4.5 4.5V9H5a2 2 0 00-2 2v6a2 2 0 002 2h10a2 2 0 002-2v-6a2 2 0 00-2-2h-.5V5.5A4.5 4.5 0 0010 1zm3 8V5.5a3 3 0 10-6 0V9h6z" clipRule="evenodd" />
                            </svg>
                            <h1 className="text-3xl font-bold text-transparent bg-clip-text bg-gradient-to-r from-cyan-400 to-blue-500">
                                {passwordIsSet ? 'ورود به پنل' : 'ایمن‌سازی پنل'}
                            </h1>
                             <p className="text-gray-400 mt-2">
                                {passwordIsSet ? 'برای دسترسی به پنل، رمز عبور خود را وارد کنید.' : 'برای کنترل پنل یک رمز عبور امن تعیین کنید.'}
                            </p>
                        </div>
                        
                        <div>
                            <label htmlFor="password" className="block text-sm font-medium text-gray-300 mb-2">رمز عبور</label>
                            <input
                                id="password"
                                type="password"
                                value={password}
                                onChange={(e) => setPassword(e.target.value)}
                                required
                                className="w-full bg-gray-700 text-white border border-gray-600 rounded-md p-3 focus:ring-2 focus:ring-cyan-500 focus:border-cyan-500 transition text-left"
                                dir="ltr"
                            />
                        </div>

                        {!passwordIsSet && (
                            <div>
                                <label htmlFor="confirmPassword" className="block text-sm font-medium text-gray-300 mb-2">تکرار رمز عبور</label>
                                <input
                                    id="confirmPassword"
                                    type="password"
                                    value={confirmPassword}
                                    onChange={(e) => setConfirmPassword(e.target.value)}
                                    required
                                     className="w-full bg-gray-700 text-white border border-gray-600 rounded-md p-3 focus:ring-2 focus:ring-cyan-500 focus:border-cyan-500 transition text-left"
                                    dir="ltr"
                                />
                            </div>
                        )}
                        
                        {error && <p className="text-red-400 text-sm text-center bg-red-900/30 p-3 rounded-md border border-red-500/50">{error}</p>}

                        <button
                            type="submit"
                            disabled={isLoading}
                            className="w-full mt-2 px-6 py-3 bg-gradient-to-r from-cyan-500 to-blue-600 hover:from-cyan-600 hover:to-blue-700 text-white font-bold rounded-md transition-all duration-300 transform hover:scale-105 shadow-lg disabled:opacity-50 disabled:cursor-wait"
                        >
                            {isLoading ? 'در حال پردازش...' : (passwordIsSet ? 'ورود' : 'تنظیم رمز و ورود')}
                        </button>
                    </form>
                </div>
            );
        };
        
        // --- from App.tsx ---
        const App = () => {
            const {
                config,
                isEditing,
                updatePhoneNumber,
                updateKey,
                updateSirenCommand,
                toggleEditMode,
                login,
                setPassword,
                addKey,
                removeKey
            } = useAlarmConfig();
            
            const [isAuthenticated, setIsAuthenticated] = useState(!config.passwordHash);

            const handleSendCommand = useCallback((command) => {
                if (!config.phoneNumber) {
                    alert('لطفاً ابتدا شماره تلفن دزدگیر را وارد کنید.');
                    return;
                }
                if (!command) {
                    alert('دستور ارسالی خالی است. لطفاً یک دستور معتبر وارد کنید.');
                    return;
                }
                const smsLink = `sms:${config.phoneNumber}?body=${encodeURIComponent(command)}`;
                window.location.href = smsLink;
            }, [config.phoneNumber]);
            
            const handleLogin = useCallback(async (password) => {
                const success = await login(password);
                if (success) {
                    setIsAuthenticated(true);
                }
                return success;
            }, [login]);

            const handleSetPassword = useCallback(async (password) => {
                await setPassword(password);
                setIsAuthenticated(true);
            }, [setPassword]);
            
            const handleLogout = () => {
                setIsAuthenticated(false);
                if (isEditing) {
                    toggleEditMode();
                }
            };

            if (!isAuthenticated) {
                return (
                     <div className="min-h-screen bg-gray-900 font-sans flex items-center justify-center p-4">
                        <LoginScreen 
                            passwordIsSet={!!config.passwordHash}
                            onLogin={handleLogin}
                            onSetPassword={handleSetPassword}
                        />
                    </div>
                );
            }

            return (
                <div className="min-h-screen bg-gray-900 text-white font-sans p-4 sm:p-6 lg:p-8">
                    <div className="max-w-4xl mx-auto">
                        <Header />
                        <main>
                            <div className="bg-gray-800/50 backdrop-blur-sm rounded-xl p-6 mb-8 border border-gray-700 shadow-lg">
                                <div className="flex flex-col sm:flex-row gap-4 justify-between items-center">
                                   <PhoneNumberInput 
                                        phoneNumber={config.phoneNumber} 
                                        onUpdate={updatePhoneNumber} 
                                   />
                                   <div className="flex items-center gap-2 w-full sm:w-auto pt-4 sm:pt-0">
                                       <EditButton 
                                            isEditing={isEditing} 
                                            onToggle={toggleEditMode} 
                                       />
                                       <LogoutButton onLogout={handleLogout} />
                                   </div>
                                </div>
                            </div>

                            <div id="keysContainer" className="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6 mb-8">
                                {config.keys.map((key) => (
                                    <KeyControl
                                        key={key.id}
                                        keyData={key}
                                        isEditing={isEditing}
                                        onUpdate={(field, value) => updateKey(key.id, field, value)}
                                        onSendCommand={handleSendCommand}
                                        onRemove={removeKey}
                                    />
                                ))}
                            </div>

                            {isEditing && (
                                <div className="flex justify-center mb-8">
                                    <button
                                        onClick={addKey}
                                        className="px-6 py-3 bg-gradient-to-r from-blue-500 to-cyan-600 hover:from-blue-600 hover:to-cyan-700 text-white rounded-md font-semibold transition-all duration-300 transform hover:scale-105 shadow-lg flex items-center justify-center gap-2"
                                    >
                                         <svg xmlns="http://www.w3.org/2000/svg" className="h-5 w-5" viewBox="0 0 20 20" fill="currentColor">
                                            <path fillRule="evenodd" d="M10 5a1 1 0 011 1v3h3a1 1 0 110 2h-3v3a1 1 0 11-2 0v-3H6a1 1 0 110-2h3V6a1 1 0 011-1z" clipRule="evenodd" />
                                        </svg>
                                        <span>افزودن کلید جدید</span>
                                    </button>
                                </div>
                            )}

                            <SirenControl 
                                sirenCommand={config.sirenCommand}
                                isEditing={isEditing}
                                onUpdate={updateSirenCommand}
                                onSendCommand={handleSendCommand}
                            />

                            <ManualAlarm />
                        </main>
                        <Footer />
                    </div>
                </div>
            );
        };
        
        // --- from index.tsx ---
        const rootElement = document.getElementById('root');
        if (!rootElement) {
          throw new Error("Could not find root element to mount to");
        }

        const root = ReactDOM.createRoot(rootElement);
        root.render(
          <React.StrictMode>
            <App />
          </React.StrictMode>
        );

    </script>
<script type="module" src="/index.tsx"></script>
</body>
</html>
