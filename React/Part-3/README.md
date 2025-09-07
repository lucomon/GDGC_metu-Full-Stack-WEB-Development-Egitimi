# React İleri Seviye - Eğitim Materyali

> **Eğitmen:** Faruk Bora Güvenkaya  
> **Süre:** 6-8 hafta  
> **Seviye:** İleri  
> **Ön Gereksinimler:** React Orta Seviye, JavaScript İleri Seviye

## 📋 İçindekiler

- [State Management (Redux)](#state-management-redux)
- [Redux Toolkit (RTK Query)](#redux-toolkit-rtk-query)
- [React Query / TanStack Query](#react-query--tanstack-query)
- [Server-Side Rendering (Next.js)](#server-side-rendering-nextjs)
- [Static Site Generation (SSG)](#static-site-generation-ssg)
- [React Testing](#react-testing)
- [TypeScript ile React](#typescript-ile-react)
- [React Performance Profiling](#react-performance-profiling)
- [React DevTools](#react-devtools)
- [React 18+ Features](#react-18-features)
- [Suspense ve Error Boundaries](#suspense-ve-error-boundaries)
- [React Server Components](#react-server-components)
- [Modern Build Tools](#modern-build-tools)
- [Deployment](#deployment)

---

## 🗃️ State Management (Redux)

Redux, uygulamanın state'ini merkezi bir store'da yönetir. Büyük uygulamalarda state yönetimini kolaylaştırır.

### Redux Temel Kavramlar
```javascript
// store.js
import { createStore } from 'redux';

// Action types
const INCREMENT = 'INCREMENT';
const DECREMENT = 'DECREMENT';
const RESET = 'RESET';

// Action creators
export const increment = () => ({ type: INCREMENT });
export const decrement = () => ({ type: DECREMENT });
export const reset = () => ({ type: RESET });

// Reducer
function counterReducer(state = { count: 0 }, action) {
    switch (action.type) {
        case INCREMENT:
            return { count: state.count + 1 };
        case DECREMENT:
            return { count: state.count - 1 };
        case RESET:
            return { count: 0 };
        default:
            return state;
    }
}

// Store
export const store = createStore(counterReducer);
```

### React-Redux Kullanımı
```javascript
// App.js
import { Provider } from 'react-redux';
import { store } from './store';
import Counter from './Counter';

function App() {
    return (
        <Provider store={store}>
            <Counter />
        </Provider>
    );
}

// Counter.js
import { useSelector, useDispatch } from 'react-redux';
import { increment, decrement, reset } from './store';

function Counter() {
    const count = useSelector(state => state.count);
    const dispatch = useDispatch();
    
    return (
        <div>
            <h2>Sayı: {count}</h2>
            <button onClick={() => dispatch(increment())}>Artır</button>
            <button onClick={() => dispatch(decrement())}>Azalt</button>
            <button onClick={() => dispatch(reset())}>Sıfırla</button>
        </div>
    );
}
```

### Karmaşık Redux State
```javascript
// store.js
const ADD_TODO = 'ADD_TODO';
const TOGGLE_TODO = 'TOGGLE_TODO';
const DELETE_TODO = 'DELETE_TODO';
const SET_FILTER = 'SET_FILTER';

export const addTodo = (text) => ({
    type: ADD_TODO,
    payload: { id: Date.now(), text, completed: false }
});

export const toggleTodo = (id) => ({
    type: TOGGLE_TODO,
    payload: id
});

export const deleteTodo = (id) => ({
    type: DELETE_TODO,
    payload: id
});

export const setFilter = (filter) => ({
    type: SET_FILTER,
    payload: filter
});

const initialState = {
    todos: [],
    filter: 'all'
};

function todoReducer(state = initialState, action) {
    switch (action.type) {
        case ADD_TODO:
            return {
                ...state,
                todos: [...state.todos, action.payload]
            };
        case TOGGLE_TODO:
            return {
                ...state,
                todos: state.todos.map(todo =>
                    todo.id === action.payload
                        ? { ...todo, completed: !todo.completed }
                        : todo
                )
            };
        case DELETE_TODO:
            return {
                ...state,
                todos: state.todos.filter(todo => todo.id !== action.payload)
            };
        case SET_FILTER:
            return {
                ...state,
                filter: action.payload
            };
        default:
            return state;
    }
}

export const store = createStore(todoReducer);
```

---

## 🛠️ Redux Toolkit (RTK Query)

Redux Toolkit, Redux'u daha basit hale getirir ve RTK Query ile API yönetimi sağlar.

### RTK Store Kurulumu
```javascript
// store.js
import { configureStore } from '@reduxjs/toolkit';
import { apiSlice } from './api/apiSlice';
import counterSlice from './features/counter/counterSlice';

export const store = configureStore({
    reducer: {
        counter: counterSlice,
        [apiSlice.reducerPath]: apiSlice.reducer,
    },
    middleware: (getDefaultMiddleware) =>
        getDefaultMiddleware().concat(apiSlice.middleware),
});

// counterSlice.js
import { createSlice } from '@reduxjs/toolkit';

const counterSlice = createSlice({
    name: 'counter',
    initialState: { value: 0 },
    reducers: {
        increment: (state) => {
            state.value += 1;
        },
        decrement: (state) => {
            state.value -= 1;
        },
        incrementByAmount: (state, action) => {
            state.value += action.payload;
        },
    },
});

export const { increment, decrement, incrementByAmount } = counterSlice.actions;
export default counterSlice.reducer;
```

### RTK Query API Slice
```javascript
// api/apiSlice.js
import { createApi, fetchBaseQuery } from '@reduxjs/toolkit/query/react';

export const apiSlice = createApi({
    reducerPath: 'api',
    baseQuery: fetchBaseQuery({
        baseUrl: '/api',
        prepareHeaders: (headers, { getState }) => {
            const token = getState().auth.token;
            if (token) {
                headers.set('authorization', `Bearer ${token}`);
            }
            return headers;
        },
    }),
    tagTypes: ['User', 'Post'],
    endpoints: (builder) => ({
        getUsers: builder.query({
            query: () => 'users',
            providesTags: ['User'],
        }),
        getUser: builder.query({
            query: (id) => `users/${id}`,
            providesTags: (result, error, id) => [{ type: 'User', id }],
        }),
        createUser: builder.mutation({
            query: (user) => ({
                url: 'users',
                method: 'POST',
                body: user,
            }),
            invalidatesTags: ['User'],
        }),
        updateUser: builder.mutation({
            query: ({ id, ...user }) => ({
                url: `users/${id}`,
                method: 'PUT',
                body: user,
            }),
            invalidatesTags: (result, error, { id }) => [{ type: 'User', id }],
        }),
        deleteUser: builder.mutation({
            query: (id) => ({
                url: `users/${id}`,
                method: 'DELETE',
            }),
            invalidatesTags: (result, error, id) => [{ type: 'User', id }],
        }),
    }),
});

export const {
    useGetUsersQuery,
    useGetUserQuery,
    useCreateUserMutation,
    useUpdateUserMutation,
    useDeleteUserMutation,
} = apiSlice;
```

### RTK Query Kullanımı
```javascript
// UserList.js
import { useGetUsersQuery, useDeleteUserMutation } from '../api/apiSlice';

function UserList() {
    const { data: users, error, isLoading } = useGetUsersQuery();
    const [deleteUser] = useDeleteUserMutation();
    
    if (isLoading) return <div>Yükleniyor...</div>;
    if (error) return <div>Hata: {error.message}</div>;
    
    const handleDelete = async (id) => {
        try {
            await deleteUser(id).unwrap();
        } catch (error) {
            console.error('Kullanıcı silinemedi:', error);
        }
    };
    
    return (
        <div>
            <h2>Kullanıcılar</h2>
            <ul>
                {users?.map(user => (
                    <li key={user.id}>
                        <h3>{user.name}</h3>
                        <p>{user.email}</p>
                        <button onClick={() => handleDelete(user.id)}>
                            Sil
                        </button>
                    </li>
                ))}
            </ul>
        </div>
    );
}
```

---

## 🔄 React Query / TanStack Query

React Query, server state yönetimi için güçlü bir kütüphanedir.

### React Query Kurulumu
```javascript
// App.js
import { QueryClient, QueryClientProvider } from '@tanstack/react-query';
import { ReactQueryDevtools } from '@tanstack/react-query-devtools';

const queryClient = new QueryClient({
    defaultOptions: {
        queries: {
            staleTime: 5 * 60 * 1000, // 5 dakika
            cacheTime: 10 * 60 * 1000, // 10 dakika
            retry: 3,
            refetchOnWindowFocus: false,
        },
    },
});

function App() {
    return (
        <QueryClientProvider client={queryClient}>
            <UserList />
            <ReactQueryDevtools initialIsOpen={false} />
        </QueryClientProvider>
    );
}
```

### Temel Query Kullanımı
```javascript
// hooks/useUsers.js
import { useQuery, useMutation, useQueryClient } from '@tanstack/react-query';

const fetchUsers = async () => {
    const response = await fetch('/api/users');
    if (!response.ok) {
        throw new Error('Kullanıcılar yüklenemedi');
    }
    return response.json();
};

export const useUsers = () => {
    return useQuery({
        queryKey: ['users'],
        queryFn: fetchUsers,
    });
};

export const useUser = (id) => {
    return useQuery({
        queryKey: ['users', id],
        queryFn: async () => {
            const response = await fetch(`/api/users/${id}`);
            if (!response.ok) {
                throw new Error('Kullanıcı yüklenemedi');
            }
            return response.json();
        },
        enabled: !!id,
    });
};
```

### Mutation Kullanımı
```javascript
// hooks/useUserMutations.js
export const useCreateUser = () => {
    const queryClient = useQueryClient();
    
    return useMutation({
        mutationFn: async (userData) => {
            const response = await fetch('/api/users', {
                method: 'POST',
                headers: { 'Content-Type': 'application/json' },
                body: JSON.stringify(userData),
            });
            if (!response.ok) {
                throw new Error('Kullanıcı oluşturulamadı');
            }
            return response.json();
        },
        onSuccess: () => {
            queryClient.invalidateQueries({ queryKey: ['users'] });
        },
    });
};

export const useUpdateUser = () => {
    const queryClient = useQueryClient();
    
    return useMutation({
        mutationFn: async ({ id, ...userData }) => {
            const response = await fetch(`/api/users/${id}`, {
                method: 'PUT',
                headers: { 'Content-Type': 'application/json' },
                body: JSON.stringify(userData),
            });
            if (!response.ok) {
                throw new Error('Kullanıcı güncellenemedi');
            }
            return response.json();
        },
        onSuccess: (data) => {
            queryClient.invalidateQueries({ queryKey: ['users'] });
            queryClient.invalidateQueries({ queryKey: ['users', data.id] });
        },
    });
};
```

### Infinite Query
```javascript
// hooks/useInfiniteUsers.js
export const useInfiniteUsers = () => {
    return useInfiniteQuery({
        queryKey: ['users', 'infinite'],
        queryFn: async ({ pageParam = 1 }) => {
            const response = await fetch(`/api/users?page=${pageParam}&limit=10`);
            if (!response.ok) {
                throw new Error('Kullanıcılar yüklenemedi');
            }
            return response.json();
        },
        getNextPageParam: (lastPage) => {
            return lastPage.hasNextPage ? lastPage.nextPage : undefined;
        },
    });
};

// InfiniteUserList.js
function InfiniteUserList() {
    const {
        data,
        fetchNextPage,
        hasNextPage,
        isFetchingNextPage,
        isLoading,
        error,
    } = useInfiniteUsers();
    
    if (isLoading) return <div>Yükleniyor...</div>;
    if (error) return <div>Hata: {error.message}</div>;
    
    return (
        <div>
            {data?.pages.map((page, i) => (
                <div key={i}>
                    {page.users.map(user => (
                        <div key={user.id}>
                            <h3>{user.name}</h3>
                            <p>{user.email}</p>
                        </div>
                    ))}
                </div>
            ))}
            {hasNextPage && (
                <button
                    onClick={() => fetchNextPage()}
                    disabled={isFetchingNextPage}
                >
                    {isFetchingNextPage ? 'Yükleniyor...' : 'Daha Fazla Yükle'}
                </button>
            )}
        </div>
    );
}
```

---

## ⚡ Server-Side Rendering (Next.js)

Next.js, React uygulamaları için full-stack framework'tür.

### Next.js Kurulumu
```bash
npx create-next-app@latest my-app
cd my-app
npm run dev
```

### Pages Router
```javascript
// pages/index.js
export default function Home({ posts }) {
    return (
        <div>
            <h1>Ana Sayfa</h1>
            <ul>
                {posts.map(post => (
                    <li key={post.id}>
                        <h2>{post.title}</h2>
                        <p>{post.excerpt}</p>
                    </li>
                ))}
            </ul>
        </div>
    );
}

export async function getServerSideProps() {
    const res = await fetch('https://api.example.com/posts');
    const posts = await res.json();
    
    return {
        props: { posts },
    };
}
```

### Static Generation
```javascript
// pages/posts/[id].js
export default function Post({ post }) {
    return (
        <div>
            <h1>{post.title}</h1>
            <p>{post.content}</p>
        </div>
    );
}

export async function getStaticPaths() {
    const res = await fetch('https://api.example.com/posts');
    const posts = await res.json();
    
    const paths = posts.map(post => ({
        params: { id: post.id.toString() },
    }));
    
    return {
        paths,
        fallback: false,
    };
}

export async function getStaticProps({ params }) {
    const res = await fetch(`https://api.example.com/posts/${params.id}`);
    const post = await res.json();
    
    return {
        props: { post },
        revalidate: 60, // 60 saniyede bir yeniden oluştur
    };
}
```

### App Router (Next.js 13+)
```javascript
// app/layout.js
export const metadata = {
    title: 'My App',
    description: 'My App Description',
};

export default function RootLayout({ children }) {
    return (
        <html lang="en">
            <body>
                <nav>
                    <Link href="/">Ana Sayfa</Link>
                    <Link href="/about">Hakkında</Link>
                </nav>
                {children}
            </body>
        </html>
    );
}

// app/page.js
async function getPosts() {
    const res = await fetch('https://api.example.com/posts', {
        next: { revalidate: 60 }
    });
    return res.json();
}

export default async function Home() {
    const posts = await getPosts();
    
    return (
        <div>
            <h1>Ana Sayfa</h1>
            <ul>
                {posts.map(post => (
                    <li key={post.id}>
                        <h2>{post.title}</h2>
                        <p>{post.excerpt}</p>
                    </li>
                ))}
            </ul>
        </div>
    );
}
```

---

## 🏗️ Static Site Generation (SSG)

SSG, build time'da HTML sayfaları oluşturur.

### Next.js ile SSG
```javascript
// pages/blog/[slug].js
export default function BlogPost({ post }) {
    return (
        <article>
            <h1>{post.title}</h1>
            <div dangerouslySetInnerHTML={{ __html: post.content }} />
        </article>
    );
}

export async function getStaticPaths() {
    const res = await fetch('https://api.example.com/posts');
    const posts = await res.json();
    
    const paths = posts.map(post => ({
        params: { slug: post.slug },
    }));
    
    return {
        paths,
        fallback: 'blocking', // Yeni sayfalar için
    };
}

export async function getStaticProps({ params }) {
    const res = await fetch(`https://api.example.com/posts/${params.slug}`);
    const post = await res.json();
    
    if (!post) {
        return {
            notFound: true,
        };
    }
    
    return {
        props: { post },
        revalidate: 3600, // 1 saatte bir yeniden oluştur
    };
}
```

### Gatsby ile SSG
```javascript
// gatsby-node.js
exports.createPages = async ({ graphql, actions }) => {
    const { createPage } = actions;
    
    const result = await graphql(`
        query {
            allMarkdownRemark {
                edges {
                    node {
                        frontmatter {
                            slug
                        }
                    }
                }
            }
        }
    `);
    
    result.data.allMarkdownRemark.edges.forEach(({ node }) => {
        createPage({
            path: `/blog/${node.frontmatter.slug}`,
            component: require.resolve('./src/templates/blog-post.js'),
            context: {
                slug: node.frontmatter.slug,
            },
        });
    });
};

// src/templates/blog-post.js
import React from 'react';
import { graphql } from 'gatsby';

export default function BlogPost({ data }) {
    const { markdownRemark } = data;
    const { frontmatter, html } = markdownRemark;
    
    return (
        <div>
            <h1>{frontmatter.title}</h1>
            <div dangerouslySetInnerHTML={{ __html: html }} />
        </div>
    );
}

export const query = graphql`
    query($slug: String!) {
        markdownRemark(frontmatter: { slug: { eq: $slug } }) {
            html
            frontmatter {
                title
                date
            }
        }
    }
`;
```

---

## 🧪 React Testing

React uygulamalarını test etmek için Jest ve React Testing Library kullanılır.

### Test Kurulumu
```bash
npm install --save-dev @testing-library/react @testing-library/jest-dom @testing-library/user-event jest-environment-jsdom
```

### Component Testing
```javascript
// Button.test.js
import { render, screen, fireEvent } from '@testing-library/react';
import userEvent from '@testing-library/user-event';
import Button from './Button';

describe('Button', () => {
    test('renders button with text', () => {
        render(<Button>Click me</Button>);
        expect(screen.getByRole('button', { name: /click me/i })).toBeInTheDocument();
    });
    
    test('calls onClick when clicked', async () => {
        const handleClick = jest.fn();
        const user = userEvent.setup();
        
        render(<Button onClick={handleClick}>Click me</Button>);
        
        await user.click(screen.getByRole('button'));
        expect(handleClick).toHaveBeenCalledTimes(1);
    });
    
    test('is disabled when disabled prop is true', () => {
        render(<Button disabled>Click me</Button>);
        expect(screen.getByRole('button')).toBeDisabled();
    });
});
```

### Hook Testing
```javascript
// useCounter.test.js
import { renderHook, act } from '@testing-library/react';
import { useCounter } from './useCounter';

describe('useCounter', () => {
    test('should initialize with default value', () => {
        const { result } = renderHook(() => useCounter());
        expect(result.current.count).toBe(0);
    });
    
    test('should initialize with custom value', () => {
        const { result } = renderHook(() => useCounter(10));
        expect(result.current.count).toBe(10);
    });
    
    test('should increment count', () => {
        const { result } = renderHook(() => useCounter());
        
        act(() => {
            result.current.increment();
        });
        
        expect(result.current.count).toBe(1);
    });
    
    test('should decrement count', () => {
        const { result } = renderHook(() => useCounter(5));
        
        act(() => {
            result.current.decrement();
        });
        
        expect(result.current.count).toBe(4);
    });
});
```

### Integration Testing
```javascript
// TodoApp.test.js
import { render, screen, fireEvent, waitFor } from '@testing-library/react';
import userEvent from '@testing-library/user-event';
import TodoApp from './TodoApp';

describe('TodoApp', () => {
    test('adds new todo', async () => {
        const user = userEvent.setup();
        render(<TodoApp />);
        
        const input = screen.getByPlaceholderText(/add new todo/i);
        const addButton = screen.getByRole('button', { name: /add/i });
        
        await user.type(input, 'New todo');
        await user.click(addButton);
        
        expect(screen.getByText('New todo')).toBeInTheDocument();
    });
    
    test('toggles todo completion', async () => {
        const user = userEvent.setup();
        render(<TodoApp />);
        
        const todoText = screen.getByText('Test todo');
        await user.click(todoText);
        
        expect(todoText).toHaveStyle('text-decoration: line-through');
    });
    
    test('deletes todo', async () => {
        const user = userEvent.setup();
        render(<TodoApp />);
        
        const deleteButton = screen.getByRole('button', { name: /delete/i });
        await user.click(deleteButton);
        
        expect(screen.queryByText('Test todo')).not.toBeInTheDocument();
    });
});
```

---

## 📘 TypeScript ile React

TypeScript, React uygulamalarında tip güvenliği sağlar.

### TypeScript Kurulumu
```bash
npm install --save-dev typescript @types/react @types/react-dom
npx tsc --init
```

### Component Props Typing
```typescript
// Button.tsx
import React from 'react';

interface ButtonProps {
    children: React.ReactNode;
    onClick?: () => void;
    variant?: 'primary' | 'secondary' | 'danger';
    size?: 'small' | 'medium' | 'large';
    disabled?: boolean;
}

const Button: React.FC<ButtonProps> = ({
    children,
    onClick,
    variant = 'primary',
    size = 'medium',
    disabled = false,
}) => {
    return (
        <button
            onClick={onClick}
            disabled={disabled}
            className={`btn btn-${variant} btn-${size}`}
        >
            {children}
        </button>
    );
};

export default Button;
```

### State ve Hook Typing
```typescript
// useCounter.ts
import { useState, useCallback } from 'react';

interface UseCounterReturn {
    count: number;
    increment: () => void;
    decrement: () => void;
    reset: () => void;
}

export const useCounter = (initialValue: number = 0): UseCounterReturn => {
    const [count, setCount] = useState<number>(initialValue);
    
    const increment = useCallback(() => {
        setCount(prev => prev + 1);
    }, []);
    
    const decrement = useCallback(() => {
        setCount(prev => prev - 1);
    }, []);
    
    const reset = useCallback(() => {
        setCount(initialValue);
    }, [initialValue]);
    
    return { count, increment, decrement, reset };
};
```

### API Typing
```typescript
// types/api.ts
export interface User {
    id: number;
    name: string;
    email: string;
    age: number;
    createdAt: string;
}

export interface CreateUserRequest {
    name: string;
    email: string;
    age: number;
}

export interface UpdateUserRequest extends Partial<CreateUserRequest> {
    id: number;
}

export interface ApiResponse<T> {
    data: T;
    message: string;
    success: boolean;
}

// hooks/useUsers.ts
import { useState, useEffect } from 'react';
import { User, CreateUserRequest, UpdateUserRequest } from '../types/api';

export const useUsers = () => {
    const [users, setUsers] = useState<User[]>([]);
    const [loading, setLoading] = useState<boolean>(true);
    const [error, setError] = useState<string | null>(null);
    
    const fetchUsers = async (): Promise<void> => {
        try {
            setLoading(true);
            setError(null);
            const response = await fetch('/api/users');
            const data: User[] = await response.json();
            setUsers(data);
        } catch (err) {
            setError(err instanceof Error ? err.message : 'Bilinmeyen hata');
        } finally {
            setLoading(false);
        }
    };
    
    const createUser = async (userData: CreateUserRequest): Promise<User> => {
        const response = await fetch('/api/users', {
            method: 'POST',
            headers: { 'Content-Type': 'application/json' },
            body: JSON.stringify(userData),
        });
        
        if (!response.ok) {
            throw new Error('Kullanıcı oluşturulamadı');
        }
        
        const newUser: User = await response.json();
        setUsers(prev => [...prev, newUser]);
        return newUser;
    };
    
    const updateUser = async (userData: UpdateUserRequest): Promise<User> => {
        const response = await fetch(`/api/users/${userData.id}`, {
            method: 'PUT',
            headers: { 'Content-Type': 'application/json' },
            body: JSON.stringify(userData),
        });
        
        if (!response.ok) {
            throw new Error('Kullanıcı güncellenemedi');
        }
        
        const updatedUser: User = await response.json();
        setUsers(prev => prev.map(user => 
            user.id === userData.id ? updatedUser : user
        ));
        return updatedUser;
    };
    
    useEffect(() => {
        fetchUsers();
    }, []);
    
    return {
        users,
        loading,
        error,
        createUser,
        updateUser,
        refetch: fetchUsers,
    };
};
```

---

## 📊 React Performance Profiling

React uygulamalarının performansını ölçmek ve optimize etmek için çeşitli araçlar kullanılır.

### React Profiler
```javascript
import { Profiler } from 'react';

function onRenderCallback(id, phase, actualDuration, baseDuration, startTime, commitTime) {
    console.log('Profiler:', {
        id,
        phase,
        actualDuration,
        baseDuration,
        startTime,
        commitTime,
    });
}

function App() {
    return (
        <Profiler id="App" onRender={onRenderCallback}>
            <ExpensiveComponent />
        </Profiler>
    );
}
```

### Performance Monitoring
```javascript
// utils/performance.js
export const measurePerformance = (name, fn) => {
    const start = performance.now();
    const result = fn();
    const end = performance.now();
    
    console.log(`${name} took ${end - start} milliseconds`);
    return result;
};

// Component'te kullanım
function ExpensiveComponent({ data }) {
    const processedData = useMemo(() => {
        return measurePerformance('Data Processing', () => {
            return data.map(item => ({
                ...item,
                processed: item.value * 2
            }));
        });
    }, [data]);
    
    return (
        <div>
            {processedData.map(item => (
                <div key={item.id}>{item.processed}</div>
            ))}
        </div>
    );
}
```

### Bundle Analysis
```javascript
// webpack.config.js
const BundleAnalyzerPlugin = require('webpack-bundle-analyzer').BundleAnalyzerPlugin;

module.exports = {
    plugins: [
        new BundleAnalyzerPlugin({
            analyzerMode: 'static',
            openAnalyzer: false,
        }),
    ],
};

// package.json
{
    "scripts": {
        "analyze": "npm run build && npx webpack-bundle-analyzer build/static/js/*.js"
    }
}
```

---

## 🔧 React DevTools

React DevTools, React uygulamalarını debug etmek için kullanılır.

### DevTools Kurulumu
```bash
# Chrome Extension
https://chrome.google.com/webstore/detail/react-developer-tools/fmkadmapgofadopljbjfkapdkoienihi

# Firefox Add-on
https://addons.mozilla.org/en-US/firefox/addon/react-devtools/
```

### DevTools Kullanımı
```javascript
// Component'lerde debug bilgisi
function UserProfile({ user }) {
    // DevTools'ta görünecek
    console.log('UserProfile rendered with:', user);
    
    return (
        <div>
            <h2>{user.name}</h2>
            <p>{user.email}</p>
        </div>
    );
}

// Performance profiling
function ExpensiveComponent({ data }) {
    const [processedData, setProcessedData] = useState([]);
    
    useEffect(() => {
        const start = performance.now();
        
        const processed = data.map(item => ({
            ...item,
            processed: item.value * 2
        }));
        
        setProcessedData(processed);
        
        const end = performance.now();
        console.log(`Processing took ${end - start} milliseconds`);
    }, [data]);
    
    return (
        <div>
            {processedData.map(item => (
                <div key={item.id}>{item.processed}</div>
            ))}
        </div>
    );
}
```

---

## 🚀 React 18+ Features

React 18 ile gelen yeni özellikler.

### Concurrent Features
```javascript
import { startTransition, useTransition } from 'react';

function App() {
    const [input, setInput] = useState('');
    const [list, setList] = useState([]);
    const [isPending, startTransition] = useTransition();
    
    const handleInputChange = (e) => {
        setInput(e.target.value);
        
        // Bu güncelleme düşük öncelikli
        startTransition(() => {
            setList(Array.from({ length: 10000 }, (_, i) => ({
                id: i,
                text: `Item ${i}`
            })));
        });
    };
    
    return (
        <div>
            <input value={input} onChange={handleInputChange} />
            {isPending && <div>Yükleniyor...</div>}
            <ul>
                {list.map(item => (
                    <li key={item.id}>{item.text}</li>
                ))}
            </ul>
        </div>
    );
}
```

### Suspense ile Data Fetching
```javascript
import { Suspense } from 'react';

function UserProfile({ userId }) {
    const user = use(fetchUser(userId)); // use hook (experimental)
    
    return (
        <div>
            <h2>{user.name}</h2>
            <p>{user.email}</p>
        </div>
    );
}

function App() {
    return (
        <Suspense fallback={<div>Kullanıcı yükleniyor...</div>}>
            <UserProfile userId={1} />
        </Suspense>
    );
}
```

### Automatic Batching
```javascript
function App() {
    const [count, setCount] = useState(0);
    const [flag, setFlag] = useState(false);
    
    const handleClick = () => {
        // React 18'de bu otomatik olarak batch'lenir
        setCount(c => c + 1);
        setFlag(f => !f);
        // Sadece bir re-render olur
    };
    
    return (
        <div>
            <button onClick={handleClick}>
                Count: {count}, Flag: {flag.toString()}
            </button>
        </div>
    );
}
```

---

## ⏳ Suspense ve Error Boundaries

Suspense ve Error Boundaries, React'te hata yönetimi ve loading state'leri için kullanılır.

### Suspense ile Lazy Loading
```javascript
import { Suspense, lazy } from 'react';

const LazyComponent = lazy(() => import('./LazyComponent'));

function App() {
    return (
        <Suspense fallback={<div>Component yükleniyor...</div>}>
            <LazyComponent />
        </Suspense>
    );
}
```

### Error Boundary ile Suspense
```javascript
import { ErrorBoundary } from 'react-error-boundary';

function ErrorFallback({ error, resetErrorBoundary }) {
    return (
        <div role="alert">
            <h2>Bir hata oluştu!</h2>
            <pre>{error.message}</pre>
            <button onClick={resetErrorBoundary}>Tekrar Dene</button>
        </div>
    );
}

function App() {
    return (
        <ErrorBoundary
            FallbackComponent={ErrorFallback}
            onError={(error, errorInfo) => {
                console.error('Error Boundary yakaladı:', error, errorInfo);
            }}
        >
            <Suspense fallback={<div>Yükleniyor...</div>}>
                <LazyComponent />
            </Suspense>
        </ErrorBoundary>
    );
}
```

---

## 🖥️ React Server Components

React Server Components, server-side rendering'in gelişmiş versiyonudur.

### Server Component
```javascript
// app/users/page.js (Server Component)
import { db } from '@/lib/db';

async function getUsers() {
    const users = await db.user.findMany();
    return users;
}

export default async function UsersPage() {
    const users = await getUsers();
    
    return (
        <div>
            <h1>Kullanıcılar</h1>
            <ul>
                {users.map(user => (
                    <li key={user.id}>
                        <h3>{user.name}</h3>
                        <p>{user.email}</p>
                    </li>
                ))}
            </ul>
        </div>
    );
}
```

### Client Component ile Server Component
```javascript
// app/users/page.js (Server Component)
import UserList from './UserList';
import UserActions from './UserActions';

export default async function UsersPage() {
    const users = await getUsers();
    
    return (
        <div>
            <h1>Kullanıcılar</h1>
            <UserList users={users} />
            <UserActions />
        </div>
    );
}

// app/users/UserList.js (Server Component)
export default function UserList({ users }) {
    return (
        <ul>
            {users.map(user => (
                <li key={user.id}>
                    <h3>{user.name}</h3>
                    <p>{user.email}</p>
                </li>
            ))}
        </ul>
    );
}

// app/users/UserActions.js (Client Component)
'use client';

import { useState } from 'react';

export default function UserActions() {
    const [count, setCount] = useState(0);
    
    return (
        <div>
            <button onClick={() => setCount(count + 1)}>
                Count: {count}
            </button>
        </div>
    );
}
```

---

## 🛠️ Modern Build Tools

Modern React uygulamaları için build araçları.

### Vite
```javascript
// vite.config.js
import { defineConfig } from 'vite';
import react from '@vitejs/plugin-react';

export default defineConfig({
    plugins: [react()],
    server: {
        port: 3000,
        open: true,
    },
    build: {
        outDir: 'dist',
        sourcemap: true,
    },
    optimizeDeps: {
        include: ['react', 'react-dom'],
    },
});
```

### Webpack 5
```javascript
// webpack.config.js
const path = require('path');
const HtmlWebpackPlugin = require('html-webpack-plugin');

module.exports = {
    entry: './src/index.js',
    output: {
        path: path.resolve(__dirname, 'dist'),
        filename: '[name].[contenthash].js',
        clean: true,
    },
    module: {
        rules: [
            {
                test: /\.(js|jsx)$/,
                exclude: /node_modules/,
                use: {
                    loader: 'babel-loader',
                    options: {
                        presets: ['@babel/preset-env', '@babel/preset-react'],
                    },
                },
            },
            {
                test: /\.css$/,
                use: ['style-loader', 'css-loader'],
            },
        ],
    },
    plugins: [
        new HtmlWebpackPlugin({
            template: './public/index.html',
        }),
    ],
    resolve: {
        extensions: ['.js', '.jsx'],
    },
};
```

---

## 🚀 Deployment

React uygulamalarını production'a deploy etme.

### Vercel Deployment
```bash
# Vercel CLI kurulumu
npm i -g vercel

# Deploy
vercel

# Production deploy
vercel --prod
```

### Netlify Deployment
```bash
# Netlify CLI kurulumu
npm i -g netlify-cli

# Deploy
netlify deploy

# Production deploy
netlify deploy --prod
```

### Docker ile Deployment
```dockerfile
# Dockerfile
FROM node:18-alpine

WORKDIR /app

COPY package*.json ./
RUN npm ci --only=production

COPY . .
RUN npm run build

FROM nginx:alpine
COPY --from=0 /app/dist /usr/share/nginx/html
COPY nginx.conf /etc/nginx/nginx.conf

EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
```

```yaml
# docker-compose.yml
version: '3.8'
services:
  app:
    build: .
    ports:
      - "80:80"
    environment:
      - NODE_ENV=production
```

---

## 🎯 Özet

Bu eğitim materyalinde React'in ileri seviye konularını öğrendik:

- **State Management** - Redux, Zustand, Jotai
- **Redux Toolkit** - RTK Query ile API yönetimi
- **React Query** - Server state yönetimi
- **Server-Side Rendering** - Next.js ile SSR
- **Static Site Generation** - SSG teknikleri
- **React Testing** - Jest ve Testing Library
- **TypeScript ile React** - Tip güvenliği
- **Performance Profiling** - Performans optimizasyonu
- **React DevTools** - Debug araçları
- **React 18+ Features** - Yeni özellikler
- **Suspense ve Error Boundaries** - Hata yönetimi
- **React Server Components** - Server-side rendering
- **Modern Build Tools** - Vite, Webpack
- **Deployment** - Production'a çıkarma

Bu konularla artık enterprise-level React uygulamaları geliştirebilirsiniz.
