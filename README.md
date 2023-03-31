import React, { createContext, useContext, useReducer } from "react";
import {
  UActions,
  userReducer,
  initialUsersState
} from "./Reducers/UserReducer";
import "./styles.css";
import {
  CActions,
  clientReducer,
  initialClientsState
} from "./Reducers/ClientReducer";
interface ContextType {
  usersState: {
    usersList: {
      title: string;
      id: number;
    }[];
  };
  clientsState: {
    clientsList: {
      title: string;
      id: number;
    }[];
  };
  usersDispatch: React.Dispatch<UActions>;
  clientsDispatch: React.Dispatch<CActions>;
}

const AppContext = createContext<ContextType>({
  usersState: initialUsersState,
  clientsState: initialClientsState,
  usersDispatch: () => {},
  clientsDispatch: () => {}
});

const Home = () => {
  const data = useContext(AppContext);
  return (
    <div>
      <button
        onClick={() => {
          data.clientsDispatch({
            type: "ADD_CLIENT",
            payload: { title: "Balaji", id: 1 }
          });
        }}
      >
        ADD CLIENT
      </button>
      <button
        onClick={() => {
          data.clientsDispatch({
            type: "ADD_CLIENT",
            payload: { title: "Pavan", id: 1 }
          });
        }}
      >
        ADD USER
      </button>
      {JSON.stringify(data)}
    </div>
  );
};

export default function App() {
  const [usersState, usersDispatch] = useReducer(
    userReducer,
    initialUsersState
  );
  const [clientsState, clientsDispatch] = useReducer(
    clientReducer,
    initialClientsState
  );

  return (
    <AppContext.Provider
      value={{ usersState, usersDispatch, clientsState, clientsDispatch }}
    >
      <Home />
    </AppContext.Provider>
  );
}
