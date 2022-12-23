<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <link rel="stylesheet" href="./css/main.css">
    <title>Document</title>
    <script src="https://cdn.jsdelivr.net/npm/@popperjs/core@2.11.6/dist/umd/popper.min.js"
        integrity="sha384-oBqDVmMz9ATKxIep9tiCxS/Z9fNfEXiDAYTujMAeBAsjFuCZSmKbSSUnQlmh/jp3" crossorigin="anonymous">
    </script>
    <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.2.3/dist/js/bootstrap.min.js"
        integrity="sha384-cuYeSxntonz0PPNlHhBs68uyIAVpIIOZZ5JqeqvYYIcEL727kskC66kF92t6Xl2V" crossorigin="anonymous">
    </script>
</head>

<body>
    <!-- component -->
    <div x-data="setup()" x-init="$refs.loading.classList.add('hidden');" @resize.window="watchScreen()">
        <div class="flex h-screen antialiased text-gray-900 bg-gray-100 dark:bg-dark dark:text-light">
            <!-- Loading screen -->
            <div x-ref="loading"
                class="fixed inset-0 z-50 flex items-center justify-center text-2xl font-semibold text-gray-600 bg-gray-800">
                Loading.....
            </div>

            <!-- Sidebar -->
            <div class="flex flex-shrink-0 transition-all">
                <div x-show="isSidebarOpen" @click="isSidebarOpen = false"
                    class="fixed inset-0 z-10 bg-black bg-opacity-50 lg:hidden"></div>
                <div x-show="isSidebarOpen" class="fixed inset-y-0 z-10 w-16 bg-white"></div>


                <!-- Mobile bottom bar -->
                <nav aria-label="Options"
                    class="fixed inset-x-0 bottom-0 flex flex-row-reverse items-center justify-between px-4 py-2 bg-white border-t border-gray-100 sm:hidden shadow-t rounded-t-3xl">
                    <!-- Menu button -->
                    <button
                        @click="(isSidebarOpen && currentSidebarTab == 'linksTab') ? isSidebarOpen = false : isSidebarOpen = true; currentSidebarTab = 'linksTab'"
                        class="p-2 transition-colors rounded-lg shadow-md hover:bg-gray-800 hover:text-gray-600 focus:outline-none focus:ring focus:ring-gray-600 focus:ring-offset-white focus:ring-offset-2"
                        :class="(isSidebarOpen && currentSidebarTab == 'linksTab') ? 'text-gray-600 bg-gray-600' : 'text-gray-500 bg-white'">
                        <span class="sr-only">Toggle sidebar</span>
                        <svg aria-hidden="true" class="w-6 h-6" xmlns="http://www.w3.org/2000/svg" fill="none"
                            viewBox="0 0 24 24" stroke="currentColor">
                            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
                                d="M4 6h16M4 12h16M4 18h7" />
                        </svg>
                    </button>

                    <!-- Logo  reponsive -->
                    <a href="#" class="no-underline">
                        LOGO
                    </a>
                    <!-- User avatar button -->
                    <div class="relative flex items-center flex-shrink-0 p-2" x-data="{ isOpen: false }">
                        <button @click="isOpen = !isOpen; $nextTick(() => {isOpen ? $refs.userMenu.focus() : null})"
                            class="transition-opacity rounded-lg opacity-80 hover:opacity-100 focus:outline-none focus:ring focus:ring-gray-600 focus:ring-offset-white focus:ring-offset-2">
                            <img class="w-8 h-8 rounded-lg shadow-md" src="./components/img/logo-chuan-20.png"
                                alt="Ahmed Kamel" />
                            <!-- Logo reponsive -->
                            <span class="sr-only">User menu</span>
                        </button>
                        <div x-show="isOpen" @click.away="isOpen = false" @keydown.escape="isOpen = false"
                            x-ref="userMenu" tabindex="-1"
                            class="absolute w-48 py-1 mt-2 origin-bottom-left bg-white rounded-md shadow-lg left-10 bottom-14 focus:outline-none"
                            role="menu" aria-orientation="vertical" aria-label="user menu">
                            <a href="#" class="block px-4 py-2 text-sm text-gray-700 hover:bg-gray-100"
                                role="menuitem">Your Profile</a>

                            <a href="#" class="block px-4 py-2 text-sm text-gray-700 hover:bg-gray-100"
                                role="menuitem">Settings</a>

                            <a href="#" class="block px-4 py-2 text-sm text-gray-700 hover:bg-gray-100"
                                role="menuitem">Sign out</a>
                        </div>
                    </div>
                </nav>

                <!-- Left mini bar -->
                <nav aria-label="Options"
                    class="z-20 flex-col items-center flex-shrink-0 hidden w-16 py-4 bg-white border-r-2 border-gray-100 shadow-md sm:flex ">
                    <!-- Logo -->
                    <div class="flex-shrink-0 py-4">
                        <a href="#" class="no-underline">
                            LOGO
                        </a>
                    </div>
                    <div class="flex flex-col items-center flex-1 p-2 space-y-4">
                        <!-- Menu button -->
                        <button
                            @click="(isSidebarOpen && currentSidebarTab == 'linksTab') ? isSidebarOpen = false : isSidebarOpen = true; currentSidebarTab = 'linksTab'"
                            class="p-2 transition-colors rounded-lg shadow-md hover:bg-gray-800 hover:text-gray-600 focus:outline-none focus:ring focus:ring-gray-600 focus:ring-offset-white focus:ring-offset-2"
                            :class="(isSidebarOpen && currentSidebarTab == 'linksTab') ? 'text-gray-600 bg-gray-600' : 'text-gray-500 bg-white'">
                            <span class="sr-only">Toggle sidebar</span>
                            <svg aria-hidden="true" class="w-6 h-6" xmlns="http://www.w3.org/2000/svg" fill="none"
                                viewBox="0 0 24 24" stroke="currentColor">
                                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
                                    d="M4 6h16M4 12h16M4 18h7" />
                            </svg>
                        </button>
                        <!-- Messages button -->
                        <button
                            @click="(isSidebarOpen && currentSidebarTab == 'messagesTab') ? isSidebarOpen = false : isSidebarOpen = true; currentSidebarTab = 'messagesTab'"
                            class="p-2 transition-colors rounded-lg shadow-md hover:bg-gray-800 hover:text-gray-600 focus:outline-none focus:ring focus:ring-gray-600 focus:ring-offset-white focus:ring-offset-2"
                            :class="(isSidebarOpen && currentSidebarTab == 'messagesTab') ? 'text-gray-600 bg-gray-600' : 'text-gray-500 bg-white'">
                            <span class="sr-only">Toggle message panel 1</span>
                            <svg aria-hidden="true" class="w-6 h-6" xmlns="http://www.w3.org/2000/svg" fill="none"
                                viewBox="0 0 24 24" stroke="currentColor">
                                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
                                    d="M8 10h.01M12 10h.01M16 10h.01M9 16H5a2 2 0 01-2-2V6a2 2 0 012-2h14a2 2 0 012 2v8a2 2 0 01-2 2h-5l-5 5v-5z" />
                            </svg>
                        </button>
                        <!-- Notifications button -->
                        <button
                            @click="(isSidebarOpen && currentSidebarTab == 'notificationsTab') ? isSidebarOpen = false : isSidebarOpen = true; currentSidebarTab = 'notificationsTab'"
                            class="p-2 transition-colors rounded-lg shadow-md hover:bg-gray-800 hover:text-gray-600 focus:outline-none focus:ring focus:ring-gray-600 focus:ring-offset-white focus:ring-offset-2"
                            :class="(isSidebarOpen && currentSidebarTab == 'notificationsTab') ? 'text-gray-600 bg-gray-600' : 'text-gray-500 bg-white'">
                            <span class="sr-only">Toggle notifications panel</span>
                            <svg aria-hidden="true" class="w-6 h-6" xmlns="http://www.w3.org/2000/svg" fill="none"
                                viewBox="0 0 24 24" stroke="currentColor">
                                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
                                    d="M15 17h5l-1.405-1.405A2.032 2.032 0 0118 14.158V11a6.002 6.002 0 00-4-5.659V5a2 2 0 10-4 0v.341C7.67 6.165 6 8.388 6 11v3.159c0 .538-.214 1.055-.595 1.436L4 17h5m6 0v1a3 3 0 11-6 0v-1m6 0H9" />
                            </svg>
                        </button>
                    </div>

                    <!-- User avatar -->
                    <div class="relative flex items-center flex-shrink-0 p-2" x-data="{ isOpen: false }">
                        <button @click="isOpen = !isOpen; $nextTick(() => {isOpen ? $refs.userMenu.focus() : null})"
                            class="transition-opacity rounded-lg opacity-80 hover:opacity-100 focus:outline-none focus:ring focus:ring-gray-600 focus:ring-offset-white focus:ring-offset-2">
                            <img class="w-10 h-10 rounded-lg shadow-md" src="./components/img/logo-chuan-20.png"
                                alt="Ahmed Kamel" />
                            <span class="sr-only">User menu</span>
                        </button>
                        <div x-show="isOpen" @click.away="isOpen = false" @keydown.escape="isOpen = false"
                            x-ref="userMenu" tabindex="-1"
                            class="absolute w-48 py-1 mt-2 origin-bottom-left bg-white rounded-md shadow-lg left-10 bottom-14 focus:outline-none"
                            role="menu" aria-orientation="vertical" aria-label="user menu">
                            <a href="#" class="block px-4 py-2 text-sm text-gray-700 hover:bg-gray-100"
                                role="menuitem">Your Profile</a>

                            <a href="#" class="block px-4 py-2 text-sm text-gray-700 hover:bg-gray-100"
                                role="menuitem">Settings</a>

                            <a href="./components/login/index.html"
                                class="block px-4 py-2 text-sm text-gray-700 hover:bg-gray-100" role="menuitem">Sign
                                out</a>
                        </div>
                    </div>
                </nav>

                <div x-transition:enter="transform transition-transform duration-300"
                    x-transition:enter-start="-translate-x-full" x-transition:enter-end="translate-x-0"
                    x-transition:leave="transform transition-transform duration-300"
                    x-transition:leave-start="translate-x-0" x-transition:leave-end="-translate-x-full"
                    x-show="isSidebarOpen"
                    class="fixed inset-y-0 left-0 z-10 flex-shrink-0 w-64 bg-white border-r-2 border-gray-100 shadow-lg sm:left-16 rounded-tr-3xl rounded-br-3xl sm:w-72 lg:static lg:w-64">
                    <nav x-show="currentSidebarTab == 'linksTab'" aria-label="Main" class="flex flex-col h-full">
                        <!-- Logo -->
                        <div class="flex items-center justify-center flex-shrink-0 py-10">
                            <a href="#" class="no-underline">
                                LOGO
                            </a>
                        </div>

                        <!-- Links -->
                        <ul class="flex-1 px-4 space-y-2 overflow-hidden hover:overflow-auto" id="tabs-tab"
                            role="tablist">
                            <li class="nav-item" role="presentation">
                                <a href="#tabs-home"
                                    class="flex items-center space-x-2 text-gray-600 transition-colors rounded-lg group hover:bg-gray-600 hover:text-gray-600 shadow-sm no-underline"
                                    id="tabs-home-tab" data-bs-toggle="pill" data-bs-target="#tabs-home" role="tab"
                                    aria-controls="tabs-home" aria-selected="true">
                                    <span aria-hidden="true"
                                        class="p-2 transition-colors rounded-lg group-hover:bg-gray-700 group-hover:text-gray-600">
                                        <svg class="w-6 h-6" xmlns="http://www.w3.org/2000/svg" fill="none"
                                            viewBox="0 0 24 24" stroke="currentColor">
                                            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
                                                d="M3 12l2-2m0 0l7-7 7 7M5 10v10a1 1 0 001 1h3m10-11l2 2m-2-2v10a1 1 0 01-1 1h-3m-6 0a1 1 0 001-1v-4a1 1 0 011-1h2a1 1 0 011 1v4a1 1 0 001 1m-6 0h6" />
                                        </svg>
                                    </span>
                                    <span>Trang Chủ</span>
                                </a>
                            </li>
                            <li class="nav-item" role="presentation">
                                <a href="#tabs-khoa"
                                    class="flex items-center space-x-2 text-gray-600 transition-colors rounded-lg group hover:bg-gray-600 hover:text-gray-600 shadow-sm no-underline"
                                    id="tabs-khoa-tab" data-bs-toggle="pill" data-bs-target="#tabs-khoa" role="tab"
                                    aria-controls="tabs-khoa" aria-selected="false">

                                    <span aria-hidden="true"
                                        class="p-2 transition-colors rounded-lg group-hover:bg-gray-700 group-hover:text-gray-600">
                                        <svg class="w-6 h-6" xmlns="http://www.w3.org/2000/svg" fill="none"
                                            viewBox="0 0 24 24" stroke="currentColor">
                                            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
                                                d="M7 21h10a2 2 0 002-2V9.414a1 1 0 00-.293-.707l-5.414-5.414A1 1 0 0012.586 3H7a2 2 0 00-2 2v14a2 2 0 002 2z" />
                                        </svg>
                                    </span>
                                    <span>Khoa</span>
                                </a>
                            </li>
                            <li class="nav-item" role="presentation">
                                <a href="#tabs-lop"
                                    class="flex items-center space-x-2 text-gray-600 transition-colors rounded-lg group hover:bg-gray-600 hover:text-gray-600 shadow-sm no-underline"
                                    id="tabs-lop-tab" data-bs-toggle="pill" data-bs-target="#tabs-lop" role="tab"
                                    aria-controls="tabs-lop" aria-selected="false">

                                    <span aria-hidden="true"
                                        class="p-2 transition-colors rounded-lg group-hover:bg-gray-700 group-hover:text-gray-600">
                                        <svg class="w-6 h-6" xmlns="http://www.w3.org/2000/svg" fill="none"
                                            viewBox="0 0 24 24" stroke="currentColor">
                                            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
                                                d="M7 21h10a2 2 0 002-2V9.414a1 1 0 00-.293-.707l-5.414-5.414A1 1 0 0012.586 3H7a2 2 0 00-2 2v14a2 2 0 002 2z" />
                                        </svg>
                                    </span>
                                    <span>Lớp</span>
                                </a>
                            </li>
                            <li class="nav-item" role="presentation">
                                <a href="#tabs-sv"
                                    class="flex items-center space-x-2 text-gray-600 transition-colors rounded-lg group hover:bg-gray-600 hover:text-gray-600 shadow-sm no-underline"
                                    id="tabs-sv-tab" data-bs-toggle="pill" data-bs-target="#tabs-sv" role="tab"
                                    aria-controls="tabs-sv" aria-selected="false">

                                    <span aria-hidden="true"
                                        class="p-2 transition-colors rounded-lg group-hover:bg-gray-700 group-hover:text-gray-600">
                                        <svg class="w-6 h-6" xmlns="http://www.w3.org/2000/svg" fill="none"
                                            viewBox="0 0 24 24" stroke="currentColor">
                                            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
                                                d="M7 21h10a2 2 0 002-2V9.414a1 1 0 00-.293-.707l-5.414-5.414A1 1 0 0012.586 3H7a2 2 0 00-2 2v14a2 2 0 002 2z" />
                                        </svg>
                                    </span>
                                    <span>Sinh Viên</span>
                                </a>
                            </li>
                            <li class="nav-item" role="presentation">
                                <a href="#tabs-gv"
                                    class="flex items-center space-x-2 text-gray-600 transition-colors rounded-lg group hover:bg-gray-600 hover:text-gray-600 shadow-sm no-underline"
                                    id="tabs-gv-tab" data-bs-toggle="pill" data-bs-target="#tabs-gv" role="tab"
                                    aria-controls="tabs-gv" aria-selected="false">

                                    <span aria-hidden="true"
                                        class="p-2 transition-colors rounded-lg group-hover:bg-gray-700 group-hover:text-gray-600">
                                        <svg class="w-6 h-6" xmlns="http://www.w3.org/2000/svg" fill="none"
                                            viewBox="0 0 24 24" stroke="currentColor">
                                            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
                                                d="M7 21h10a2 2 0 002-2V9.414a1 1 0 00-.293-.707l-5.414-5.414A1 1 0 0012.586 3H7a2 2 0 00-2 2v14a2 2 0 002 2z" />
                                        </svg>
                                    </span>
                                    <span>Quản Lý Giảng Viên</span>
                                </a>
                            </li>
                            <li class="nav-item" role="presentation">
                                <a href="#tabs-mh"
                                    class="flex items-center space-x-2 text-gray-600 transition-colors rounded-lg group hover:bg-gray-600 hover:text-gray-600 shadow-sm no-underline"
                                    id="tabs-mh-tab" data-bs-toggle="pill" data-bs-target="#tabs-mh" role="tab"
                                    aria-controls="tabs-mh" aria-selected="false">

                                    <span aria-hidden="true"
                                        class="p-2 transition-colors rounded-lg group-hover:bg-gray-700 group-hover:text-gray-600">
                                        <svg class="w-6 h-6" xmlns="http://www.w3.org/2000/svg" fill="none"
                                            viewBox="0 0 24 24" stroke="currentColor">
                                            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
                                                d="M7 21h10a2 2 0 002-2V9.414a1 1 0 00-.293-.707l-5.414-5.414A1 1 0 0012.586 3H7a2 2 0 00-2 2v14a2 2 0 002 2z" />
                                        </svg>
                                    </span>
                                    <span>Quản Lý Môn Học</span>
                                </a>
                            </li>
                            <li class="nav-item" role="presentation">
                                <a href="#tabs-diem"
                                    class="flex items-center space-x-2 text-gray-600 transition-colors rounded-lg group hover:bg-gray-600 hover:text-gray-600 shadow-sm no-underline"
                                    id="tabs-diem-tab" data-bs-toggle="pill" data-bs-target="#tabs-diem" role="tab"
                                    aria-controls="tabs-diem" aria-selected="false">

                                    <span aria-hidden="true"
                                        class="p-2 transition-colors rounded-lg group-hover:bg-gray-700 group-hover:text-gray-600">
                                        <svg class="w-6 h-6" xmlns="http://www.w3.org/2000/svg" fill="none"
                                            viewBox="0 0 24 24" stroke="currentColor">
                                            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
                                                d="M7 21h10a2 2 0 002-2V9.414a1 1 0 00-.293-.707l-5.414-5.414A1 1 0 0012.586 3H7a2 2 0 00-2 2v14a2 2 0 002 2z" />
                                        </svg>
                                    </span>
                                    <span>Quản Lý Điểm</span>
                                </a>
                            </li>
                            <li class="nav-item" role="presentation">
                                <a href="#tabs-thanhvien"
                                    class="flex items-center space-x-2 text-gray-600 transition-colors rounded-lg group hover:bg-gray-600 hover:text-gray-600 shadow-sm no-underline"
                                    id="tabs-thanhvien-tab" data-bs-toggle="pill" data-bs-target="#tabs-thanhvien"
                                    role="tab" aria-controls="tabs-thanhvien" aria-selected="false">

                                    <span aria-hidden="true"
                                        class="p-2 transition-colors rounded-lg group-hover:bg-gray-700 group-hover:text-gray-600">
                                        <svg class="w-6 h-6" xmlns="http://www.w3.org/2000/svg" fill="none"
                                            viewBox="0 0 24 24" stroke="currentColor">
                                            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
                                                d="M7 21h10a2 2 0 002-2V9.414a1 1 0 00-.293-.707l-5.414-5.414A1 1 0 0012.586 3H7a2 2 0 00-2 2v14a2 2 0 002 2z" />
                                        </svg>
                                    </span>
                                    <span>Thành Viên</span>
                                </a>
                            </li>
                            <li class="nav-item" role="presentation">
                                <a href="#tabs-vaitro"
                                    class="flex items-center space-x-2 text-gray-600 transition-colors rounded-lg group hover:bg-gray-600 hover:text-gray-600 shadow-sm no-underline"
                                    id="tabs-vaitro-tab" data-bs-toggle="pill" data-bs-target="#tabs-vaitro" role="tab"
                                    aria-controls="tabs-vaitro" aria-selected="false">

                                    <span aria-hidden="true"
                                        class="p-2 transition-colors rounded-lg group-hover:bg-gray-700 group-hover:text-gray-600">
                                        <svg class="w-6 h-6" xmlns="http://www.w3.org/2000/svg" fill="none"
                                            viewBox="0 0 24 24" stroke="currentColor">
                                            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
                                                d="M7 21h10a2 2 0 002-2V9.414a1 1 0 00-.293-.707l-5.414-5.414A1 1 0 0012.586 3H7a2 2 0 00-2 2v14a2 2 0 002 2z" />
                                        </svg>
                                    </span>
                                    <span>Vai Trò Của Thành Viên</span>
                                </a>
                            </li>

                        </ul>

                    </nav>

                    <section x-show="currentSidebarTab == 'messagesTab'" class="px-4 py-6">
                        <h2 class="text-xl">Messages</h2>
                    </section>

                    <section x-show="currentSidebarTab == 'notificationsTab'" class="px-4 py-6">
                        <h2 class="text-xl">Notifications</h2>
                    </section>
                </div>
            </div>
            <div class="flex flex-col flex-1">
                <header class="relative flex items-center justify-between flex-shrink-0 p-4">
                    <form action="#" class="flex-1">
                        <!--  -->
                    </form>
                    <div class="items-center hidden ml-4 sm:flex">
                        <button @click="isSettingsPanelOpen = true"
                            class="p-2 mr-4 text-gray-400 bg-white rounded-lg shadow-md hover:text-gray-600 focus:outline-none focus:ring focus:ring-white focus:ring-offset-gray-100 focus:ring-offset-4">
                            <span class="sr-only">Settings</span>
                            <svg aria-hidden="true" class="w-6 h-6" xmlns="http://www.w3.org/2000/svg" fill="none"
                                viewBox="0 0 24 24" stroke="currentColor">
                                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
                                    d="M10.325 4.317c.426-1.756 2.924-1.756 3.35 0a1.724 1.724 0 002.573 1.066c1.543-.94 3.31.826 2.37 2.37a1.724 1.724 0 001.065 2.572c1.756.426 1.756 2.924 0 3.35a1.724 1.724 0 00-1.066 2.573c.94 1.543-.826 3.31-2.37 2.37a1.724 1.724 0 00-2.572 1.065c-.426 1.756-2.924 1.756-3.35 0a1.724 1.724 0 00-2.573-1.066c-1.543.94-3.31-.826-2.37-2.37a1.724 1.724 0 00-1.065-2.572c-1.756-.426-1.756-2.924 0-3.35a1.724 1.724 0 001.066-2.573c-.94-1.543.826-3.31 2.37-2.37.996.608 2.296.07 2.572-1.065z" />
                                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
                                    d="M15 12a3 3 0 11-6 0 3 3 0 016 0z" />
                            </svg>
                        </button>

                        <!-- Github link -->
                        <a href="https://github.com/kamona-ui/dashboard-alpine" target="_blank"
                            class="p-2 text-gray-600 bg-black rounded-lg shadow-md hover:text-gray-200 focus:outline-none focus:ring focus:ring-black focus:ring-offset-gray-100 focus:ring-offset-2">
                            <span class="sr-only">github link</span>
                            <svg aria-hidden="true" class="w-6 h-6" fill="currentColor"
                                xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24">
                                <path fill-rule="evenodd" clip-rule="evenodd"
                                    d="M12.026,2c-5.509,0-9.974,4.465-9.974,9.974c0,4.406,2.857,8.145,6.821,9.465 c0.499,0.09,0.679-0.217,0.679-0.481c0-0.237-0.008-0.865-0.011-1.696c-2.775,0.602-3.361-1.338-3.361-1.338 c-0.452-1.152-1.107-1.459-1.107-1.459c-0.905-0.619,0.069-0.605,0.069-0.605c1.002,0.07,1.527,1.028,1.527,1.028 c0.89,1.524,2.336,1.084,2.902,0.829c0.091-0.645,0.351-1.085,0.635-1.334c-2.214-0.251-4.542-1.107-4.542-4.93 c0-1.087,0.389-1.979,1.024-2.675c-0.101-0.253-0.446-1.268,0.099-2.64c0,0,0.837-0.269,2.742,1.021 c0.798-0.221,1.649-0.332,2.496-0.336c0.849,0.004,1.701,0.115,2.496,0.336c1.906-1.291,2.742-1.021,2.742-1.021 c0.545,1.372,0.203,2.387,0.099,2.64c0.64,0.696,1.024,1.587,1.024,2.675c0,3.833-2.33,4.675-4.552,4.922 c0.355,0.308,0.675,0.916,0.675,1.846c0,1.334-0.012,2.41-0.012,2.737c0,0.267,0.178,0.577,0.687,0.479 C19.146,20.115,22,16.379,22,11.974C22,6.465,17.535,2,12.026,2z">
                                </path>
                            </svg>
                        </a>
                    </div>

                    <!-- Mobile sub header button -->
                    <button @click="isSubHeaderOpen = !isSubHeaderOpen"
                        class="p-2 text-gray-400 bg-white rounded-lg shadow-md sm:hidden hover:text-gray-600 focus:outline-none focus:ring focus:ring-white focus:ring-offset-gray-100 focus:ring-offset-4">
                        <span class="sr-only">More</span>

                        <svg aria-hidden="true" class="w-6 h-6" xmlns="http://www.w3.org/2000/svg" fill="none"
                            viewBox="0 0 24 24" stroke="currentColor">
                            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
                                d="M12 5v.01M12 12v.01M12 19v.01M12 6a1 1 0 110-2 1 1 0 010 2zm0 7a1 1 0 110-2 1 1 0 010 2zm0 7a1 1 0 110-2 1 1 0 010 2z" />
                        </svg>
                    </button>

                    <!-- Mobile sub header -->
                    <div x-transition:enter="transform transition-transform"
                        x-transition:enter-start="translate-y-full opacity-0"
                        x-transition:enter-end="translate-y-0 opacity-100"
                        x-transition:leave="transform transition-transform"
                        x-transition:leave-start="translate-y-0 opacity-100"
                        x-transition:leave-end="translate-y-full opacity-0" x-show="isSubHeaderOpen"
                        @click.away="isSubHeaderOpen = false"
                        class="absolute flex items-center justify-between p-2 bg-white rounded-md shadow-lg sm:hidden top-16 left-5 right-5">
                        <!-- Seetings button -->
                        <button @click="isSettingsPanelOpen = true; isSubHeaderOpen = false"
                            class="p-2 text-gray-400 bg-white rounded-lg shadow-md hover:text-gray-600 focus:outline-none focus:ring focus:ring-white focus:ring-offset-gray-100 focus:ring-offset-4">
                            <span class="sr-only">Settings</span>
                            <svg aria-hidden="true" class="w-6 h-6" xmlns="http://www.w3.org/2000/svg" fill="none"
                                viewBox="0 0 24 24" stroke="currentColor">
                                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
                                    d="M10.325 4.317c.426-1.756 2.924-1.756 3.35 0a1.724 1.724 0 002.573 1.066c1.543-.94 3.31.826 2.37 2.37a1.724 1.724 0 001.065 2.572c1.756.426 1.756 2.924 0 3.35a1.724 1.724 0 00-1.066 2.573c.94 1.543-.826 3.31-2.37 2.37a1.724 1.724 0 00-2.572 1.065c-.426 1.756-2.924 1.756-3.35 0a1.724 1.724 0 00-2.573-1.066c-1.543.94-3.31-.826-2.37-2.37a1.724 1.724 0 00-1.065-2.572c-1.756-.426-1.756-2.924 0-3.35a1.724 1.724 0 001.066-2.573c-.94-1.543.826-3.31 2.37-2.37.996.608 2.296.07 2.572-1.065z" />
                                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
                                    d="M15 12a3 3 0 11-6 0 3 3 0 016 0z" />
                            </svg>
                        </button>
                        <!-- Messages button -->
                        <button
                            @click="isSidebarOpen = true; currentSidebarTab = 'messagesTab'; isSubHeaderOpen = false"
                            class="p-2 text-gray-400 bg-white rounded-lg shadow-md hover:text-gray-600 focus:outline-none focus:ring focus:ring-white focus:ring-offset-gray-100 focus:ring-offset-4">
                            <span class="sr-only">Toggle message panel</span>
                            <svg aria-hidden="true" class="w-6 h-6" xmlns="http://www.w3.org/2000/svg" fill="none"
                                viewBox="0 0 24 24" stroke="currentColor">
                                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
                                    d="M8 10h.01M12 10h.01M16 10h.01M9 16H5a2 2 0 01-2-2V6a2 2 0 012-2h14a2 2 0 012 2v8a2 2 0 01-2 2h-5l-5 5v-5z" />
                            </svg>
                        </button>
                        <!-- Notifications button -->
                        <button
                            @click="isSidebarOpen = true; currentSidebarTab = 'notificationsTab'; isSubHeaderOpen = false"
                            class="p-2 text-gray-400 bg-white rounded-lg shadow-md hover:text-gray-600 focus:outline-none focus:ring focus:ring-white focus:ring-offset-gray-100 focus:ring-offset-4">
                            <span class="sr-only">Toggle notifications panel</span>
                            <svg aria-hidden="true" class="w-6 h-6" xmlns="http://www.w3.org/2000/svg" fill="none"
                                viewBox="0 0 24 24" stroke="currentColor">
                                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
                                    d="M15 17h5l-1.405-1.405A2.032 2.032 0 0118 14.158V11a6.002 6.002 0 00-4-5.659V5a2 2 0 10-4 0v.341C7.67 6.165 6 8.388 6 11v3.159c0 .538-.214 1.055-.595 1.436L4 17h5m6 0v1a3 3 0 11-6 0v-1m6 0H9" />
                            </svg>
                        </button>
                        <!-- Github link -->
                        <a href="#" target="_blank"
                            class="p-2 text-gray-600 bg-black rounded-lg shadow-md hover:text-gray-200 focus:outline-none focus:ring focus:ring-black focus:ring-offset-gray-100 focus:ring-offset-2">
                            <span class="sr-only">github link</span>
                            <svg aria-hidden="true" class="w-6 h-6" fill="currentColor"
                                xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24">
                                <path fill-rule="evenodd" clip-rule="evenodd"
                                    d="M12.026,2c-5.509,0-9.974,4.465-9.974,9.974c0,4.406,2.857,8.145,6.821,9.465 c0.499,0.09,0.679-0.217,0.679-0.481c0-0.237-0.008-0.865-0.011-1.696c-2.775,0.602-3.361-1.338-3.361-1.338 c-0.452-1.152-1.107-1.459-1.107-1.459c-0.905-0.619,0.069-0.605,0.069-0.605c1.002,0.07,1.527,1.028,1.527,1.028 c0.89,1.524,2.336,1.084,2.902,0.829c0.091-0.645,0.351-1.085,0.635-1.334c-2.214-0.251-4.542-1.107-4.542-4.93 c0-1.087,0.389-1.979,1.024-2.675c-0.101-0.253-0.446-1.268,0.099-2.64c0,0,0.837-0.269,2.742,1.021 c0.798-0.221,1.649-0.332,2.496-0.336c0.849,0.004,1.701,0.115,2.496,0.336c1.906-1.291,2.742-1.021,2.742-1.021 c0.545,1.372,0.203,2.387,0.099,2.64c0.64,0.696,1.024,1.587,1.024,2.675c0,3.833-2.33,4.675-4.552,4.922 c0.355,0.308,0.675,0.916,0.675,1.846c0,1.334-0.012,2.41-0.012,2.737c0,0.267,0.178,0.577,0.687,0.479 C19.146,20.115,22,16.379,22,11.974C22,6.465,17.535,2,12.026,2z">
                                </path>
                            </svg>
                        </a>
                    </div>
                </header>
                <main class=" justify-center flex-1 px-4  pt-0">



                    <main class="tab-content" id="tabs-tabContent">
                        <div class="tab-pane fade show active" id="tabs-home" role="tabpanel"
                            aria-labelledby="tabs-home-tab">
                            <div>
                                <section class="  text-gray-600">
                                    <div class="mx-auto max-w-screen-xl ">
                                        <div class="grid grid-cols-1 gap-8 md:grid-cols-2 lg:grid-cols-3">
                                            <a class="block rounded-xl border border-gray-800 p-8 shadow-xl transition hover:border-pink-500/10 hover:shadow-pink-500/10 no-underline"
                                            href="./components/khoa/index.html"
                                            >
                                                <svg xmlns="http://www.w3.org/2000/svg" class="h-10 w-10 text-pink-500"
                                                    fill="none" viewBox="0 0 24 24" stroke="currentColor">
                                                    <path d="M12 14l9-5-9-5-9 5 9 5z" />
                                                    <path
                                                        d="M12 14l6.16-3.422a12.083 12.083 0 01.665 6.479A11.952 11.952 0 0012 20.055a11.952 11.952 0 00-6.824-2.998 12.078 12.078 0 01.665-6.479L12 14z" />
                                                    <path stroke-linecap="round" stroke-linejoin="round"
                                                        stroke-width="2"
                                                        d="M12 14l9-5-9-5-9 5 9 5zm0 0l6.16-3.422a12.083 12.083 0 01.665 6.479A11.952 11.952 0 0012 20.055a11.952 11.952 0 00-6.824-2.998 12.078 12.078 0 01.665-6.479L12 14zm-4 6v-7.5l4-2.222" />
                                                </svg>
                                                <h2 class="mt-4 text-xl font-bold text-gray-600">KHOA</h2>
                                                <div class=" mt-6 inline-flex items-center text-gray-600">
                                                    <p class="text-lg font-medium">Xem Thêm</p>
                                                    <svg xmlns="http://www.w3.org/2000/svg"
                                                        class="ml-3 h-6 w-6 transform transition-transform group-hover:translate-x-3"
                                                        fill="none" viewBox="0 0 24 24" stroke="currentColor">
                                                        <path stroke-linecap="round" stroke-linejoin="round"
                                                            stroke-width="2" d="M17 8l4 4m0 0l-4 4m4-4H3" />
                                                    </svg>
                                                </div>
                                            </a>

                                            <a class="block rounded-xl border border-gray-800 p-8 shadow-xl transition hover:border-pink-500/10 hover:shadow-pink-500/10 no-underline"
                                                href="#">
                                                <svg xmlns="http://www.w3.org/2000/svg" class="h-10 w-10 text-pink-500"
                                                    fill="none" viewBox="0 0 24 24" stroke="currentColor">
                                                    <path d="M12 14l9-5-9-5-9 5 9 5z" />
                                                    <path
                                                        d="M12 14l6.16-3.422a12.083 12.083 0 01.665 6.479A11.952 11.952 0 0012 20.055a11.952 11.952 0 00-6.824-2.998 12.078 12.078 0 01.665-6.479L12 14z" />
                                                    <path stroke-linecap="round" stroke-linejoin="round"
                                                        stroke-width="2"
                                                        d="M12 14l9-5-9-5-9 5 9 5zm0 0l6.16-3.422a12.083 12.083 0 01.665 6.479A11.952 11.952 0 0012 20.055a11.952 11.952 0 00-6.824-2.998 12.078 12.078 0 01.665-6.479L12 14zm-4 6v-7.5l4-2.222" />
                                                </svg>

                                                <h2 class="mt-4 text-xl font-bold text-gray-600">LỚP</h2>

                                                <div class=" mt-6 inline-flex items-center text-gray-600">
                                                    <p class="text-lg font-medium">Xem Thêm</p>
                                                    <svg xmlns="#"
                                                        class="ml-3 h-6 w-6 transform transition-transform group-hover:translate-x-3"
                                                        fill="none" viewBox="0 0 24 24" stroke="currentColor">
                                                        <path stroke-linecap="round" stroke-linejoin="round"
                                                            stroke-width="2" d="M17 8l4 4m0 0l-4 4m4-4H3" />
                                                    </svg>
                                                </div>
                                            </a>

                                            <a class="block rounded-xl border border-gray-800 p-8 shadow-xl transition hover:border-pink-500/10 hover:shadow-pink-500/10 no-underline"
                                                href="#">
                                                <svg xmlns="http://www.w3.org/2000/svg" class="h-10 w-10 text-pink-500"
                                                    fill="none" viewBox="0 0 24 24" stroke="currentColor">
                                                    <path d="M12 14l9-5-9-5-9 5 9 5z" />
                                                    <path
                                                        d="M12 14l6.16-3.422a12.083 12.083 0 01.665 6.479A11.952 11.952 0 0012 20.055a11.952 11.952 0 00-6.824-2.998 12.078 12.078 0 01.665-6.479L12 14z" />
                                                    <path stroke-linecap="round" stroke-linejoin="round"
                                                        stroke-width="2"
                                                        d="M12 14l9-5-9-5-9 5 9 5zm0 0l6.16-3.422a12.083 12.083 0 01.665 6.479A11.952 11.952 0 0012 20.055a11.952 11.952 0 00-6.824-2.998 12.078 12.078 0 01.665-6.479L12 14zm-4 6v-7.5l4-2.222" />
                                                </svg>

                                                <h2 class="mt-4 text-xl font-bold text-gray-600">SINH VIÊN</h2>

                                                <div class=" mt-6 inline-flex items-center text-gray-600">
                                                    <p class="text-lg font-medium">Xem Thêm</p>
                                                    <svg xmlns="http://www.w3.org/2000/svg"
                                                        class="ml-3 h-6 w-6 transform transition-transform group-hover:translate-x-3"
                                                        fill="none" viewBox="0 0 24 24" stroke="currentColor">
                                                        <path stroke-linecap="round" stroke-linejoin="round"
                                                            stroke-width="2" d="M17 8l4 4m0 0l-4 4m4-4H3" />
                                                    </svg>
                                                </div>
                                            </a>

                                            <a class="block rounded-xl border border-gray-800 p-8 shadow-xl transition hover:border-pink-500/10 hover:shadow-pink-500/10 no-underline"
                                                href="#">
                                                <svg xmlns="http://www.w3.org/2000/svg" class="h-10 w-10 text-pink-500"
                                                    fill="none" viewBox="0 0 24 24" stroke="currentColor">
                                                    <path d="M12 14l9-5-9-5-9 5 9 5z" />
                                                    <path
                                                        d="M12 14l6.16-3.422a12.083 12.083 0 01.665 6.479A11.952 11.952 0 0012 20.055a11.952 11.952 0 00-6.824-2.998 12.078 12.078 0 01.665-6.479L12 14z" />
                                                    <path stroke-linecap="round" stroke-linejoin="round"
                                                        stroke-width="2"
                                                        d="M12 14l9-5-9-5-9 5 9 5zm0 0l6.16-3.422a12.083 12.083 0 01.665 6.479A11.952 11.952 0 0012 20.055a11.952 11.952 0 00-6.824-2.998 12.078 12.078 0 01.665-6.479L12 14zm-4 6v-7.5l4-2.222" />
                                                </svg>

                                                <h2 class="mt-4 text-xl font-bold text-gray-600">MÔN HỌC</h2>

                                                <div class=" mt-6 inline-flex items-center text-gray-600">
                                                    <p class="text-lg font-medium">Xem Thêm</p>
                                                    <svg xmlns="http://www.w3.org/2000/svg"
                                                        class="ml-3 h-6 w-6 transform transition-transform group-hover:translate-x-3"
                                                        fill="none" viewBox="0 0 24 24" stroke="currentColor">
                                                        <path stroke-linecap="round" stroke-linejoin="round"
                                                            stroke-width="2" d="M17 8l4 4m0 0l-4 4m4-4H3" />
                                                    </svg>
                                                </div>
                                            </a>

                                            <a class="block rounded-xl border border-gray-800 p-8 shadow-xl transition hover:border-pink-500/10 hover:shadow-pink-500/10 no-underline"
                                                href="#">
                                                <svg xmlns="http://www.w3.org/2000/svg" class="h-10 w-10 text-pink-500"
                                                    fill="none" viewBox="0 0 24 24" stroke="currentColor">
                                                    <path d="M12 14l9-5-9-5-9 5 9 5z" />
                                                    <path
                                                        d="M12 14l6.16-3.422a12.083 12.083 0 01.665 6.479A11.952 11.952 0 0012 20.055a11.952 11.952 0 00-6.824-2.998 12.078 12.078 0 01.665-6.479L12 14z" />
                                                    <path stroke-linecap="round" stroke-linejoin="round"
                                                        stroke-width="2"
                                                        d="M12 14l9-5-9-5-9 5 9 5zm0 0l6.16-3.422a12.083 12.083 0 01.665 6.479A11.952 11.952 0 0012 20.055a11.952 11.952 0 00-6.824-2.998 12.078 12.078 0 01.665-6.479L12 14zm-4 6v-7.5l4-2.222" />
                                                </svg>

                                                <h2 class="mt-4 text-xl font-bold text-gray-600">GIẢNG VIÊN</h2>

                                                <div class=" mt-6 inline-flex items-center text-gray-600">
                                                    <p class="text-lg font-medium">Xem Thêm</p>
                                                    <svg xmlns="http://www.w3.org/2000/svg"
                                                        class="ml-3 h-6 w-6 transform transition-transform group-hover:translate-x-3"
                                                        fill="none" viewBox="0 0 24 24" stroke="currentColor">
                                                        <path stroke-linecap="round" stroke-linejoin="round"
                                                            stroke-width="2" d="M17 8l4 4m0 0l-4 4m4-4H3" />
                                                    </svg>
                                                </div>
                                            </a>


                                        </div>


                                    </div>
                                </section>

                            </div>

                        </div>
                        <div class="tab-pane fade" id="tabs-khoa" role="tabpanel" aria-labelledby="tabs-khoa-tab">
                            <div class="antialiased sans-serif bg-gray-200 h-screen">
	

                               
                                <style>
                                    [x-cloak] {
                                        display: none;
                                    }
                            
                                    [type="checkbox"] {
                                        box-sizing: border-box;
                                        padding: 0;
                                    }
                            
                                    .form-checkbox {
                                        -webkit-appearance: none;
                                        -moz-appearance: none;
                                        appearance: none;
                                        -webkit-print-color-adjust: exact;
                                        color-adjust: exact;
                                        display: inline-block;
                                        vertical-align: middle;
                                        background-origin: border-box;
                                        -webkit-user-select: none;
                                        -moz-user-select: none;
                                        -ms-user-select: none;
                                        user-select: none;
                                        flex-shrink: 0;
                                        color: currentColor;
                                        background-color: #fff;
                                        border-color: #e2e8f0;
                                        border-width: 1px;
                                        border-radius: 0.25rem;
                                        height: 1.2em;
                                        width: 1.2em;
                                    }
                            
                                    .form-checkbox:checked {
                                        background-image: url("data:image/svg+xml,%3csvg viewBox='0 0 16 16' fill='white' xmlns='http://www.w3.org/2000/svg'%3e%3cpath d='M5.707 7.293a1 1 0 0 0-1.414 1.414l2 2a1 1 0 0 0 1.414 0l4-4a1 1 0 0 0-1.414-1.414L7 8.586 5.707 7.293z'/%3e%3c/svg%3e");
                                        border-color: transparent;
                                        background-color: currentColor;
                                        background-size: 100% 100%;
                                        background-position: center;
                                        background-repeat: no-repeat;
                                    }
                                </style>
                            
                                <div class="container mx-auto py-6 px-4" x-data="datatables()" x-cloak>
                                    <h1 class="text-3xl py-4 border-b mb-10">Datatable</h1>
                            
                                    <div x-show="selectedRows.length" class="bg-teal-200 fixed top-0 left-0 right-0 z-40 w-full shadow">
                                        <div class="container mx-auto px-4 py-4">
                                            <div class="flex md:items-center">
                                                <div class="mr-4 flex-shrink-0">
                                                    <svg class="h-8 w-8 text-teal-600"  viewBox="0 0 20 20" fill="currentColor">  <path fill-rule="evenodd" d="M18 10a8 8 0 11-16 0 8 8 0 0116 0zm-7-4a1 1 0 11-2 0 1 1 0 012 0zM9 9a1 1 0 000 2v3a1 1 0 001 1h1a1 1 0 100-2v-3a1 1 0 00-1-1H9z" clip-rule="evenodd"/></svg>
                                                </div>
                                                <div x-html="selectedRows.length + ' rows are selected'" class="text-teal-800 text-lg"></div>
                                            </div>
                                        </div>
                                    </div>
                            
                                    <div class="mb-4 flex justify-between items-center">
                                        <div class="flex-1 pr-4">
                                            <div class="relative md:w-1/3">
                                                <input type="search"
                                                    class="w-full pl-10 pr-4 py-2 rounded-lg shadow focus:outline-none focus:shadow-outline text-gray-600 font-medium"
                                                    placeholder="Search...">
                                                <div class="absolute top-0 left-0 inline-flex items-center p-2">
                                                    <svg xmlns="http://www.w3.org/2000/svg" class="w-6 h-6 text-gray-400" viewBox="0 0 24 24"
                                                        stroke-width="2" stroke="currentColor" fill="none" stroke-linecap="round"
                                                        stroke-linejoin="round">
                                                        <rect x="0" y="0" width="24" height="24" stroke="none"></rect>
                                                        <circle cx="10" cy="10" r="7" />
                                                        <line x1="21" y1="21" x2="15" y2="15" />
                                                    </svg>
                                                </div>
                                            </div>
                                        </div>
                                        <div>
                                            <div class="shadow rounded-lg flex">
                                                <div class="relative">
                                                    <button @click.prevent="open = !open"
                                                        class="rounded-lg inline-flex items-center bg-white hover:text-blue-500 focus:outline-none focus:shadow-outline text-gray-500 font-semibold py-2 px-2 md:px-4">
                                                        <svg xmlns="http://www.w3.org/2000/svg" class="w-6 h-6 md:hidden" viewBox="0 0 24 24"
                                                            stroke-width="2" stroke="currentColor" fill="none" stroke-linecap="round"
                                                            stroke-linejoin="round">
                                                            <rect x="0" y="0" width="24" height="24" stroke="none"></rect>
                                                            <path
                                                                d="M5.5 5h13a1 1 0 0 1 0.5 1.5L14 12L14 19L10 16L10 12L5 6.5a1 1 0 0 1 0.5 -1.5" />
                                                        </svg>
                                                        <span class="hidden md:block">Display</span>
                                                        <svg xmlns="http://www.w3.org/2000/svg" class="w-5 h-5 ml-1" width="24" height="24"
                                                            viewBox="0 0 24 24" stroke-width="2" stroke="currentColor" fill="none"
                                                            stroke-linecap="round" stroke-linejoin="round">
                                                            <rect x="0" y="0" width="24" height="24" stroke="none"></rect>
                                                            <polyline points="6 9 12 15 18 9" />
                                                        </svg>
                                                    </button>
                            
                                                    <div x-show="open" @click.away="open = false"
                                                        class="z-40 absolute top-0 right-0 w-40 bg-white rounded-lg shadow-lg mt-12 -mr-1 block py-1 overflow-hidden">
                                                        <template x-for="heading in headings">
                                                            <label
                                                                class="flex justify-start items-center text-truncate hover:bg-gray-100 px-4 py-2">
                                                                <div class="text-teal-600 mr-3">
                                                                    <input type="checkbox" class="form-checkbox focus:outline-none focus:shadow-outline" checked @click="toggleColumn(heading.key)">
                                                                </div>
                                                                <div class="select-none text-gray-700" x-text="heading.value"></div>
                                                            </label>
                                                        </template>
                                                    </div>
                                                </div>
                                            </div>
                                        </div>
                                    </div>
                            
                                    <div class="overflow-x-auto bg-white rounded-lg shadow overflow-y-auto relative"
                                        style="height: 405px;">
                                        <table class="border-collapse table-auto w-full whitespace-no-wrap bg-white table-striped relative">
                                            <thead>
                                                <tr class="text-left">
                                                    <th class="py-2 px-3 sticky top-0 border-b border-gray-200 bg-gray-100">
                                                        <label
                                                            class="text-teal-500 inline-flex justify-between items-center hover:bg-gray-200 px-2 py-2 rounded-lg cursor-pointer">
                                                            <input type="checkbox" class="form-checkbox focus:outline-none focus:shadow-outline" @click="selectAllCheckbox($event);">
                                                        </label>
                                                    </th>
                                                    <template x-for="heading in headings">
                                                        <th class="bg-gray-100 sticky top-0 border-b border-gray-200 px-6 py-2 text-gray-600 font-bold tracking-wider uppercase text-xs"
                                                            x-text="heading.value" :x-ref="heading.key" :class="{ [heading.key]: true }"></th>
                                                    </template>
                                                </tr>
                                            </thead>
                                            <tbody>
                                                <template x-for="user in users" :key="user.userId">
                                                    <tr>
                                                        <td class="border-dashed border-t border-gray-200 px-3">
                                                            <label
                                                                class="text-teal-500 inline-flex justify-between items-center hover:bg-gray-200 px-2 py-2 rounded-lg cursor-pointer">
                                                                <input type="checkbox" class="form-checkbox rowCheckbox focus:outline-none focus:shadow-outline" :name="user.userId"
                                                                        @click="getRowDetail($event, user.userId)">
                                                            </label>
                                                        </td>
                                                        <td class="border-dashed border-t border-gray-200 userId">
                                                            <span class="text-gray-700 px-6 py-3 flex items-center" x-text="user.userId"></span>
                                                        </td>
                                                        <td class="border-dashed border-t border-gray-200 firstName">
                                                            <span class="text-gray-700 px-6 py-3 flex items-center" x-text="user.firstName"></span>
                                                        </td>
                                                        <td class="border-dashed border-t border-gray-200 lastName">
                                                            <span class="text-gray-700 px-6 py-3 flex items-center" x-text="user.lastName"></span>
                                                        </td>
                                                        <td class="border-dashed border-t border-gray-200 emailAddress">
                                                            <span class="text-gray-700 px-6 py-3 flex items-center"
                                                                x-text="user.emailAddress"></span>
                                                        </td>
                                                        <td class="border-dashed border-t border-gray-200 gender">
                                                            <span class="text-gray-700 px-6 py-3 flex items-center"
                                                                x-text="user.gender"></span>
                                                        </td>
                                                        <td class="border-dashed border-t border-gray-200 phoneNumber">
                                                            <span class="text-gray-700 px-6 py-3 flex items-center"
                                                                x-text="user.phoneNumber"></span>
                                                        </td>
                                                    </tr>
                                                </template>
                                            </tbody>
                                        </table>
                                    </div>
                                </div>
                          
                            </div>
                        </div>
                        <div class="tab-pane fade" id="tabs-lop" role="tabpanel" aria-labelledby="tabs-lop-tab">
                            Tab 3 lop
                        </div>
                        <div class="tab-pane fade" id="tabs-sv" role="tabpanel" aria-labelledby="tabs-sv-tab">
                            Tab 4 sv
                        </div>
                        <div class="tab-pane fade" id="tabs-gv" role="tabpanel" aria-labelledby="tabs-gv-tab">
                            Tab 5 gv
                        </div>
                        <div class="tab-pane fade" id="tabs-mh" role="tabpanel" aria-labelledby="tabs-mh-tab">
                            Tab 6 mh
                        </div>
                        <div class="tab-pane fade" id="tabs-diem" role="tabpanel" aria-labelledby="tabs-diem-tab">
                            Tab 7 diem
                        </div>
                        <div class="tab-pane fade" id="tabs-thanhvien" role="tabpanel"
                            aria-labelledby="tabs-thanhvien-tab">
                            Tab 8 thanhvien
                        </div>
                        <div class="tab-pane fade" id="tabs-vaitro" role="tabpanel" aria-labelledby="tabs-vaitro-tab">
                            Tab 9 content
                        </div>
                    </main>

                    <!-- Content -->
                </main>

            </div>
        </div>

        <!-- Panels -->

        <!-- Settings Panel -->
        <!-- Backdrop -->
        <div x-show="isSettingsPanelOpen" class="fixed inset-0 bg-black bg-opacity-50"
            @click="isSettingsPanelOpen = false" aria-hidden="true"></div>
        <!-- Panel -->
        <section x-transition:enter="transform transition-transform duration-300"
            x-transition:enter-start="translate-x-full" x-transition:enter-end="translate-x-0"
            x-transition:leave="transform transition-transform duration-300" x-transition:leave-start="translate-x-0"
            x-transition:leave-end="translate-x-full" x-show="isSettingsPanelOpen"
            class="fixed inset-y-0 right-0 w-64 bg-white border-l border-gray-100 rounded-l-3xl">
            <div class="px-4 py-8">
                <h2 class="text-lg font-semibold">Settings</h2>
            </div>
        </section>

        <!-- Author links -->
        <div class="fixed flex items-center space-x-4 bottom-20 right-5 sm:bottom-5">
            <a href="#" target="_blank" class="transition-transform transform hover:scale-125">
                <span class="sr-only">Twitter</span>
                <svg aria-hidden="true" class="w-8 h-8 text-blue-500" fill="currentColor"
                    xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24">
                    <path
                        d="M19.633,7.997c0.013,0.175,0.013,0.349,0.013,0.523c0,5.325-4.053,11.461-11.46,11.461c-2.282,0-4.402-0.661-6.186-1.809 c0.324,0.037,0.636,0.05,0.973,0.05c1.883,0,3.616-0.636,5.001-1.721c-1.771-0.037-3.255-1.197-3.767-2.793 c0.249,0.037,0.499,0.062,0.761,0.062c0.361,0,0.724-0.05,1.061-0.137c-1.847-0.374-3.23-1.995-3.23-3.953v-0.05 c0.537,0.299,1.16,0.486,1.82,0.511C3.534,9.419,2.823,8.184,2.823,6.787c0-0.748,0.199-1.434,0.548-2.032 c1.983,2.443,4.964,4.04,8.306,4.215c-0.062-0.3-0.1-0.611-0.1-0.923c0-2.22,1.796-4.028,4.028-4.028 c1.16,0,2.207,0.486,2.943,1.272c0.91-0.175,1.782-0.512,2.556-0.973c-0.299,0.935-0.936,1.721-1.771,2.22 c0.811-0.088,1.597-0.312,2.319-0.624C21.104,6.712,20.419,7.423,19.633,7.997z">
                    </path>
                </svg>
            </a>
            <a href="#" target="_blank" class="transition-transform transform hover:scale-125">
                <span class="sr-only">Github</span>
                <svg aria-hidden="true" class="w-8 h-8 text-black" fill="currentColor"
                    xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24">
                    <path fill-rule="evenodd" clip-rule="evenodd"
                        d="M12.026,2c-5.509,0-9.974,4.465-9.974,9.974c0,4.406,2.857,8.145,6.821,9.465 c0.499,0.09,0.679-0.217,0.679-0.481c0-0.237-0.008-0.865-0.011-1.696c-2.775,0.602-3.361-1.338-3.361-1.338 c-0.452-1.152-1.107-1.459-1.107-1.459c-0.905-0.619,0.069-0.605,0.069-0.605c1.002,0.07,1.527,1.028,1.527,1.028 c0.89,1.524,2.336,1.084,2.902,0.829c0.091-0.645,0.351-1.085,0.635-1.334c-2.214-0.251-4.542-1.107-4.542-4.93 c0-1.087,0.389-1.979,1.024-2.675c-0.101-0.253-0.446-1.268,0.099-2.64c0,0,0.837-0.269,2.742,1.021 c0.798-0.221,1.649-0.332,2.496-0.336c0.849,0.004,1.701,0.115,2.496,0.336c1.906-1.291,2.742-1.021,2.742-1.021 c0.545,1.372,0.203,2.387,0.099,2.64c0.64,0.696,1.024,1.587,1.024,2.675c0,3.833-2.33,4.675-4.552,4.922 c0.355,0.308,0.675,0.916,0.675,1.846c0,1.334-0.012,2.41-0.012,2.737c0,0.267,0.178,0.577,0.687,0.479 C19.146,20.115,22,16.379,22,11.974C22,6.465,17.535,2,12.026,2z">
                    </path>
                </svg>
            </a>
        </div>
    </div>
    </div>

    <script src="https://cdn.jsdelivr.net/gh/alpinejs/alpine@v2.7.3/dist/alpine.min.js" defer></script>
    <script>
        const setup = () => {
            return {
                isSidebarOpen: false,
                isSideBodyOpen: false,
                currentSidebarTab: null,
                currentSidebarBody: null,
                currentSidebarHome: null,
                isSettingsPanelOpen: false,
                isSubHeaderOpen: false,
                watchScreen() {
                    if (window.innerWidth <= 1024) {
                        this.isSidebarOpen = false
                    }
                },
            }
        }
    </script>
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.1.3/dist/css/bootstrap.min.css" rel="stylesheet"
        integrity="sha384-1BmE4kWBq78iYhFldvKuhfTAU6auU8tT94WrHftjDbrCEXSU1oBoqyl2QvZ6jIW3" crossorigin="anonymous">
    <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.1.3/dist/js/bootstrap.bundle.min.js"
        integrity="sha384-ka7Sk0Gln4gmtz2MlQnikT1wXgYsOg+OMhuP+IlRH9sENBO0LRn5q+8nbTov4+1p" crossorigin="anonymous">
    </script>
    <script src="./components/khoa/app.js"></script>
    <link rel="stylesheet" href="https://unpkg.com/tailwindcss@^1.0/dist/tailwind.min.css">
    <script src="https://cdn.jsdelivr.net/gh/alpinejs/alpine@v2.x.x/dist/alpine.js" defer></script>
</body>

</html>