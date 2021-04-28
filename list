#include <cstddef>
#include <iostream>

template<typename T>
class List {
private:
    struct Node_ {
        T *value;
        Node_ *prev, *next;

        Node_(T *value, Node_ *prev, Node_ *next) : value(value), prev(prev), next(next) {}

        ~Node_() {
            delete value;
        }
    } *head, *tail;

    size_t size_;


public:
    List() : head(nullptr), tail(nullptr), size_(0) {}

    List(const List &other) : head(nullptr), tail(nullptr), size_(0) {
        for (auto i = other.begin(); i != other.end(); ++i) {
            push_back(*i);
        }
    }

    List &operator=(const List &that) {
        while (size_ > 0) {
            pop_back();
        }
        for (auto i = that.begin(); i != that.end(); ++i) {
            push_back(*i);
        }
        return *this;
    }

    ~List() {
        while (size_ > 0) {
            pop_back();
        }
    }

    void push_back(const T &elem) {
        if (size_ == 0) {
            head = tail = new Node_(new T(elem), nullptr, nullptr);
        } else {
            tail = tail->next = new Node_(new T(elem), tail, nullptr);
        }
        ++size_;
    }

    void push_front(const T &elem) {
        if (size_ == 0) {
            head = tail = new Node_(new T(elem), nullptr, nullptr);
        } else {
            head = head->prev = new Node_(new T(elem), nullptr, head);
        }
        ++size_;
    }

    void pop_front() {
        Node_ *temp = head;
        head = head->next;
        if (size_ == 1) {
            tail = nullptr;
        } else {
            head->prev = nullptr;
        }
        delete temp;
        --size_;
    }

    void pop_back() {
        Node_ *temp = tail;
        tail = tail->prev;
        if (size_ == 1) {
            head = nullptr;
        } else {
            tail->next = nullptr;
        }
        delete temp;
        --size_;
    }

    size_t size() const {
        return size_;
    }

    class ConstIterator {
    private:
        const List *l;
        Node_ *n;

    public:
        ConstIterator(const List *value, Node_ *i) : l(value), n(i) {}

        ConstIterator &operator++() {
            n = n->next;
            return *this;
        }

        ConstIterator &operator--() {
            n = (n != nullptr ? n->prev : l->tail);
            return *this;
        }

        T operator*() const {
            return *(n->value);
        }


        bool operator==(const ConstIterator &that) const {
            return (n == that.n && l == that.l);
        }

        bool operator!=(const ConstIterator &that) const {
            return (n != that.n || l != that.l);
        }
    };

    ConstIterator begin() const {
        return ConstIterator(this, head);
    }

    ConstIterator end() const {
        return ConstIterator(this, tail->next);
    }
};
